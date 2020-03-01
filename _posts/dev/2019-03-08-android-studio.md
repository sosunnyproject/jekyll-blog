---
layout: post
categories: dev
title: "android studio install manual"
date: 2019-03-08T13:01:27-05:00
last_modified_at: 2019-03-09T13:01:27-05:00
share: false
---

https://developer.android.com/studio/install.html


**If you want to enter a menu, and see multiple pages instead of a single static page**
- Viewpager (in xml layout)
- Fragment 
- FragmentActivity
- FragmentStatePagerAdapter

**If you want to give different types of views as the Fragment slides**
```java
public class ScreenSlideActivity extends FragmentActivity {
  public static String inputStr = "string";
  
  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.yourLayout);
    String inputStr = getIntent().getStringExtra(URL);  // the input string you gave when you call this class, gets entered
    //some...code...
    }
  
  //some...code...
  
  private class ScreenSlidePagerAdapter extends FragmentStatePagerAdapter {
          public String inputStr1 = "first";
          public String inputStr2 = "second";
          public ScreenSlidePagerAdapter(FragmentManager fm, String str) {
              super(fm);
              String subStr = str.substring(0, str.length() -4);    // header class's STring inputStr got passed onto String str
              inputStr1 = subStr + "html";
              inputStr2 = subStr + "json";
          }

          @Override
          public Fragment getItem(int position) {
              if (position == 0) {
              //SlideOne is the 'public class SlideOne extends Fragment{ ... } 코드파일
                  SlideOne fragment = new SlideOne();
                  fragment.setInput(inputStr1);  //  use this to pass over the inputStr1 parameter to 'SlideOne' Fragment class, if you set the inputString parameter as private and made setConstructor called 'setInput' in SlideOne Class
                  return fragment;
              }
              else if {
                  SlideTwo fragment2 = new SlideTwo();
                  slideTwoInput = inputStr2; // you can pass over like this, if you set inputString parameter as public in SlideTwo Class
                  return fragment2;
              }         
          }
    }
  }
 ```

**If you want to bring the staic Webpage screen**
- use WebView
- the official instructions/manuals are pretty straightforward


**If you want to send a Toast pop up message while the app is running**
- ref: https://stackoverflow.com/questions/41729152/display-messagebody-of-firebase-notification-as-toast
- Handler: http://humble.tistory.com/14, http://itmining.tistory.com/16?category=640759
- Toast: https://developer.android.com/guide/topics/ui/notifiers/toasts.html, https://www.udemy.com/complete-android-n-developer-course/learn

**how I edited android studio files and structured the connections..**
```bash
├─.gradle
│  ├─4.1
│  │  ├─fileChanges
│  │  ├─fileContent
│  │  ├─fileHashes
│  │  ├─javaCompile
│  │  └─taskHistory
│  └─buildOutputCleanup
├─.idea
│  └─libraries
├─app
///////////////////////// (중략)
│  ├─libs
│  ├─sampledata
│  └─src
│      ├─androidTest
│      │  └─java.kr.co...
│      ├─main
│      │  ├─assets
│      │  ├─java
│      │  │  ├─ko // co..
│      │  │  └─kr
│      │  │      └─co...
|      |  |         ├─camera
│      │  │         ├─qrcode             
│      │  │         └─weather             
│      │  └─res // deleted unused ones
│      │      ├─animator
│      │      ├─drawable
│      │      ├─layout
│      │      ├─menu
│      │      ├─raw
│      │      └─xml
│      └─test // java.kr.co ...
├─build
│  ├─android-profile
│  └─intermediates
│      └─proguard-files
└─gradle
    └─wrapper
```
DIRECTORY I WORKED ON...
>> app>src>main>java>product_address.co.kr 

```bash
│      ├─main
│      │  ├─assets
│      │  ├─java
│      │  │  ├─ko // co..
│      │  │  └─kr
│      │  │      └─co...
|      |  |         ├─camera
|      |  |         ├─qrcode
|      |  |         └─weather
|      |  |         │  BaseActivity.java
|      |  |         │  CameraActivity.java
|      |  |         │  CameraPageData.java
|      |  |         │  CameraPageDataViewPagerItemFragment.java
|      |  |         │  ErrorcodeFour.java
|      |  |         │  ErrorcodeOne.java
|      |  |         │  ErrorcodeTwo.java
|      |  |         │  Glasses.java
|      |  |         │  MainActivity.java
|      |  |         │  MainPageData.java
|      |  |         │  MainPageDataViewPagerItemFragment.java
|      |  |         │  QrFragmentOne.java
|      |  |         │  QrFragmentThree.java
|      |  |         │  QrFragmentTwo.java
|      |  |         │  QrScreenSlideActivity.java
|      |  |         │
|      |  |         ├─qrcode
|      |  |         │      jsonFunction.java
|      |  |         │      QrcodeReceiver.java
|      |  |         │      QrjsonActivity.java
```

calling order
QR code recognized --> QrcodeReceiver.java runs 
```java
public class QrcodeReceiver extends BroadcastReceiver {
  @Override
    public void onReceive(Context context, Intent intent) {
      String action = intent.getAction();
      if (action.equals(ACTION_RESULT_TEXT)) {
        final String result = intent.getStringExtra(INTENT_EXTRA_RESULT_TEXT);
        if..
        else if...
        else  {
                Glasses.startQrActivity(result);
                }
        }
    }
}
```
--> Glasses.java
```java
public class Glasses extends Application{
      @Override
    public void onCreate() {
        super.onCreate();
        mContext = getApplicationContext();
        //... 생략
        // 현재 registration token 얻어오기.
        // https://firebase.google.com/docs/cloud-messaging/android/first-message?authuser=0
        String token = FirebaseInstanceId.getInstance().getToken();
        Log.d("Glasses", " FirebaseInstanceId Token: " + token);

        MyFirebaseInstanceIdService.sendRegistrationToServer(token);
    }
    // 아래는 수많은 메뉴 Activity java class 가리키는 methods
    public static void startErrorTwoActivity() {
        Intent intent = new Intent(mContext, ErrorcodeTwo.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        mContext.startActivity(intent);
    }
    public static void startErrorFourActivity() {
        Intent intent = new Intent(mContext, ErrorcodeFour.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        mContext.startActivity(intent);
    }
    public static void startErrorOneActivity() {
        Intent intent = new Intent(mContext, ErrorcodeOne.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        mContext.startActivity(intent);
    }
        public static void startQrActivity(String url) {
        Intent intent = new Intent(mContext, QrScreenSlideActivity.class);
        intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
        intent.putExtra(QrScreenSlideActivity.URL, url);  // QrcodeReceiver에서 url인자값을받아서 QrScreenSlideActivity에 전달
        mContext.startActivity(intent);
    }
        static Handler mHandler = new Handler() {
        @Override
        public void handleMessage(Message msg) {
            Toast.makeText(mContext, String.valueOf(msg.obj), msg.arg1).show();
        }
    };
        public static void showToast(CharSequence text) {
        Message msg = Message.obtain();
        msg.obj = text;
        msg.arg1 = Toast.LENGTH_SHORT;
        mHandler.sendMessage(msg);
    }
```
-->QrScreenSlideActivity.java
_QR찍고나와야하는 화면이 여러개여서 QrScreenSlideActivity parent생성해주고 여기에서 여러 fragment를 콜할것임_
```java
public class QrScreenSlideActivity extends FragmentActivity {
    private static final int NUM_PAGES = 2;
    public static String URL = "url";
    private ViewPager mPager;

    /**
     * The pager adapter, which provides the pages to the view pager widget.
     */
    private PagerAdapter mPagerAdapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.qr_screen_slide);  //  Parent XML layout
        String qrCodeUrl = getIntent().getStringExtra(URL);

        // Instantiate a ViewPager and a PagerAdapter.
        mPager = (ViewPager) findViewById(R.id.pager);
        mPagerAdapter = new ScreenSlidePagerAdapter(getSupportFragmentManager(), qrCodeUrl);
        mPager.setAdapter(mPagerAdapter);
    }
    
    private class ScreenSlidePagerAdapter extends FragmentStatePagerAdapter {
      super(fm);
      String subUrlString = url.substring(0, url.length() -4);
      qrCodeUrl = subUrlString + "html";
      qrCodeTwo = subUrlString + "json";
    }
    @Override
    public Fragment getItem(int position) {
        if (position == 0) {
            QrFragmentOne fragment = new QrFragmentOne();
            fragment.setmUrlString(qrCodeUrl);
            return fragment;
        }
        else {
            QrFragmentTwo fragment2 = new QrFragmentTwo();
            fragment2.setmUrlString(qrCodeTwo);
            return fragment2;
        }
    }

    @Override
    public int getCount() {
        return NUM_PAGES;
    }
  } 
}
```
이제여기서 Fragment1(페이지1), Fragment2(페이지2)를 call

--->Fragment1 (webview)
```java
public class QrFragmentOne extends Fragment {
    public String mUrlString = "";

    public void setmUrlString(String mUrlString) {
        this.mUrlString = mUrlString;
    }

   // public static final String QrCodeURL = QrURL;

    @Override
    public void onCreate(final Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //String jsonUrl = getIntent().getStringExtra(QrCodeURL);
        //Bundle bundle=getArguments();
        //mUrlString = bundle.getString("url", ""); //this didn't work
    }

    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        View v = inflater.inflate(R.layout.qr_frag_one, container, false);  // Child XML Layout. container prob refers to Parent one.
        WebView mWebView = (WebView) v.findViewById(R.id.webview);
        mWebView.loadUrl(mUrlString);
        mWebView.setScrollContainer(false);

        // Enable Javascript
        WebSettings webSettings = mWebView.getSettings();
        webSettings.setJavaScriptEnabled(true);

        // Force links and redirects to open in the WebView instead of in a browser
        mWebView.setWebViewClient(new WebViewClient());

        return v;
    }
}
```

--> 그다음엔Fragment2.java
```bash
public class QrFragmentTwo extends Fragment {
    public String qrCodeJson = "";
    public void setmUrlString(String mUrlString) {
            this.qrCodeJson = mUrlString; }

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        View v = inflater.inflate(R.layout.qr_frag_two, container, false);
        jsonFont = Typeface.createFromAsset(getActivity().getApplicationContext().getAssets(), "fonts/weathericons-regular-webfont.ttf");

        one = (TextView) v.findViewById(R.id.name);
        ...
        
        return v;
    }

    TextView one, two, three, four, five, six, seven, eight;
    Typeface jsonFont;
    //public static final String QrCodeURL = "http://192.168.132.113:8080/pv-operation-n-maintenance/connector_band_1.json";

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //String jsonUrl = getIntent().getStringExtra(JSON_URL);
        Log.d("큐알프레그먼트투", "온크리에이트");

        jsonFunction.placeIdTask asyncTask =new jsonFunction.placeIdTask(new jsonFunction.AsyncResponse() {
            public void processFinish(String output1,...) {
                Log.d("어씽크 배출 스트링", output1+output2+output3+output4);
                one.setText(output1);
                ...
              }
        });
        asyncTask.execute(qrCodeJson); // url address input
    }
}
```
asyncTask.execute() 하면 jsonFunction.java

```java
public class jsonFunction {

    public static String jsonURL = "";
    public interface AsyncResponse {
        void processFinish(String output1 ...);
    }

    public static class placeIdTask extends AsyncTask<String, Void, JSONObject> {
        public AsyncResponse delegate = null;//Call back interface
        public placeIdTask(AsyncResponse asyncResponse) {
            delegate = asyncResponse;//Assigning call back interface through constructor
        }

        @Override
        protected JSONObject doInBackground(String... params) {
            JSONObject myJson = null;
            try {
                Log.d("jsonFunction", params[0]);
                jsonURL = params[0];
                myJson = getMyJSON(params[0]);                  //edited since our one and only input is url address
            } catch (Exception e) {
            }
            return myJson;
        }

        @Override
        protected void onPostExecute(JSONObject json) {
            try {
                if (json != null) {
                    if (jsonURL.equals("~~.json") || jsonURL.equals("~~.json")) {
                        JSONObject info = json.getJSONObject("info");
                        JSONObject dataRotate = info.getJSONObject("data-rotate");
                        JSONObject dataChart = info.getJSONObject("data-chart");

                        // iterate through dataRotate json Object and store keys into Array
                        Iterator<String> keys = dataRotate.keys();
                        ArrayList<String> jsonKeys = new ArrayList<String>();
                        while(keys.hasNext()){
                            String key = keys.next();
                            jsonKeys.add(key);
                        }
                        String equipName = info.getString("name");
                        String date = dataChart.getString("SYS_TIME");
                        String dataOne = dataRotate.getString(jsonKeys.get(0)) ;
                        ...
                        
                        delegate.processFinish(equipName, date, dataOne, dataTwo, dataThree, dataFour, dataFive, dataSix);
                    }
                   
                    else if(jsonURL.equals("~~.json") || jsonURL.equals("~~.json")) {
                        JSONObject info = json.getJSONObject("info");
                        JSONObject dataRotate = info.getJSONObject("data-rotate");

                        // iterate through dataRotate json Object and store keys into Array
                        Iterator<String> keys = dataRotate.keys();
                        ArrayList<String> jsonKeys = new ArrayList<String>();
                        while (keys.hasNext()) {
                            String key = keys.next();
                            jsonKeys.add(key);
                        }

                        String equipName = info.getString("name");
                        String method = info.getString("method");

                        String dataOne = dataRotate.getString(jsonKeys.get(0)) + "℃";
                        ...
                        delegate.processFinish(equipName, method, dataOne, dataTwo, dataThree, dataFour, dataFive, dataSix);
                    }
                    else if(jsonURL.equals("~~~.json") || jsonURL.equals("~~~.json")) {
                        JSONObject info = json.getJSONObject("info");
                        JSONObject dataRotate = info.getJSONObject("data-rotate");
                        JSONObject dataChart = info.getJSONObject("data-chart");

                        // iterate through dataRotate json Object and store keys into Array
                        Iterator<String> keys = dataRotate.keys();
                        ArrayList<String> jsonKeys = new ArrayList<String>();
                        while (keys.hasNext()) {
                            String key = keys.next();
                            jsonKeys.add(key);
                        }
                        Log.d("placeIdTask", "onPostExecute 실행끝나고 이어서 뭔가 하겠지." + jsonKeys);


                        String equipName = info.getString("name");
                        String date = dataChart.getString("SYS_TIME");

                        String dataOne = dataRotate.getString(jsonKeys.get(0))+ " V";
                        ...
                        delegate.processFinish(equipName, date, dataOne, dataTwo, dataThree, dataFour, dataFive, dataSix);
                    }

                }
            } catch (JSONException e) {
                e.printStackTrace();
            }
        }
    }


    public static JSONObject getMyJSON(String jsonUrl){
        try {
            URL url = new URL(String.format(jsonUrl));
            HttpURLConnection connection =
                    (HttpURLConnection)url.openConnection();
            BufferedReader reader = new BufferedReader(
                    new InputStreamReader(connection.getInputStream()));
            StringBuffer json = new StringBuffer(1024);
            String tmp="";
            while((tmp=reader.readLine())!=null)
                json.append(tmp).append("\n");
            reader.close();
            JSONObject data = new JSONObject(json.toString());
            return data;
        }catch(Exception e){
            e.printStackTrace();
            return null;
        }
    }
}
```

## Android Studio - fingerprint authentification, finger touch

### Using Emulator (your android studio, emulator should be running)
1. In terminal, go to **...\Android\Sdk\platform-tools** directory
2. Find emulator number: <code> $ adb devices </code>
3. In emulator, go to **Settings > Privacy > set up passwords/pin + fingerprint** 
4. When emulator asks you to touch sensor for the first time, <code> $ adb -s emulator-5554 emu finger touch any_number </code>
5. After then, <code> $adb -e emu finger touch any_number </code>
