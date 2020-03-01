---
layout: post
categories: dev
title: "hyperledger with javascript"
date: 2018-06-10T13:01:27-05:00
share: true
---

## Javascript x Hyperledger Fabric

0. References
    - https://hyperledger.github.io/fabric-chaincode-node/
    - [API page](https://hyperledger.github.io/fabric-chaincode-node/master/api/)
    - [Chaincode tutorials](https://hyperledger-fabric.readthedocs.io/en/latest/chaincode.html)


1. Most commonly used javascript methods
    - JSON.stringify & JSON.parse
    - Fundamental functions of this code was to save JSON data into blockchain database. Thus, it had to do a lot with parsing, restructuring, replacing, and saving the data values inside JSON.

2. Things to think before you code
    - Make sure you have clear business structure, workflow of service, software architecture (like dApp) that will use this chaincode 
    - Build and draw the JSON {key: value} that will be created, modified, and saved via chaincode
    - Check if your business needs data like **JSON inside JSON**. Yes, you can still play around with it in chaincode
    - Check whether couchDB or levelDB suits your business model
    - Chaincode supports GO, Javascript, JAVA as languages. Go is known for better performance, as it actively uses the available storage and power to the max. Otherwise, choose Java or Javascript depend on your dApp environment.
    - Last but not least, Go provides local debug test without actually deploying the chaincode to your fabric server (docker environment). Java, you can compile the grammar errors in Eclipse or your IDE. Javascript, nothing I know of. 
        - This is quite important to know. Because you would test and revise your chaincode A LOT to see if you JSON data gets created/updated/saved/deleted without problem. If it causes too much hassle to go back and forth fixing and deploying the new code, it's pain in the ass. At least, it was for moi.

3. Basic template
```js
'use strict';
const shim = require('fabric-shim');
const util = require('util');
const winston = require('winston');
require('date-utils');
const moment = require('moment');
moment.locale('ko');
const fs = require('fs');

const {
  createLogger,
  format,
  transports
} = require('winston');
 
const {
  combine,
  timestamp,
  label,
  printf
} = format;


let Chaincode = class {
    async Init(stub) {
        logger.info('=========== Instantiate ===========');
        return shim.success();
    }
 
    async Invoke(stub) {
        let ret = stub.getFunctionAndParameters();
        logger.info(ret.params);
        logger.info(ret);
    
        let method = this[ret.fcn];
        if (!method) {
            logger.error('no function of name:' + ret.fcn + ' found');
            return shim.error('Received unknown function ' + ret.fcn + ' invocation');
        }
    
        try {
            let payload = await method(stub, ret.params);
            return shim.success(payload);
        } catch (err) {
            return shim.error(err);
        }
    }

    async initLedger(stub, args) {
        logger.info('============INITIALIZE LEDGER =============');
    }
 
    async create(stub, args) {
 
        // check if numbers of input argument is correct
        logger.info("raw input: " + args[0]);
        if (args.length != 1) {
            return shim.error('Incorrect number of args. Expecting 1 object');
        }

        // parse the entire JSON as key, value, etc...
        let jsonVal = JSON.parse(args[0]);
        let key = jsonVal.key;

        // check if the same key already exists in your blockchain couch db. 
        // probably you can't compare incoming and existing keys, if you use level database?
        let fileAsBytes = await stub.getState(key);
    
        // save data to DB
        await stub.putState(key, Buffer.from(JSON.stringify(content2save)));

    }

     async query(stub, args) {
         // ...
     }

     // add whatever functions, methods you need for your business 

    shim.start(new Chaincode());
```