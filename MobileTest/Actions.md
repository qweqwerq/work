<h2> Gestures </h2>

## TouchAction
## press, release
TouchAction action = new TouchAction (appiumDriver)
action.press (appiumDriver.findElement(By.id(“ID”))).perform();

Point point = appiumDriver.findElementById(“ID”).getLocation();
new TouchAction (appiumDriver).press(point.x + 10, point.y + 30).waitAction(1000).release().perform();


## long press
TouchAction action = new TouchAction (appiumDriver)
action.longPress(appiumDrver.findElement(By.id(“ID”)))).perfrom();


## move
WebElement drag = appiumDriver.findElement(By.id(“drag”));
WebElement drop = appiumDriver.findElement(By.id(“drop”));

TouchAction dragNdrop = new TouchAction(appiumDriver).longpress(drag).moveTo(drop).release();
dragNdrop.perform();


## tap
TouchAction action = new TouchAction (appiumDriver);
action.tap(appiumDriver.findElement(By.id(“ID”))).perform();


## Multi Touch
TouchAction action1 = new TouchAction (appiumDriver).tab(element1);
TouchAction action2 = new TouchAction (appiumDriver).tab(element2);

MultiTouchAction multiTouch = new MultiTouchAction(appiumDriver);
multiTouch.add(action1).add(action2).perform();




## Swipe
※ void swipe (int start_x, int start_y, int end_x, int end_y, int duration)

public void swipeLeftToright() {
  int height = drvier.manage().window().getSize().getHeight();
  int width = driver.manage().window().getSize().getWidth();

  androidDriver.swipe(width/3, height/2, (width*2)/3, height/2, 100);
}

public void swipeRightToLeft() {
  int height = drvier.manage().window().getSize().getHeight();
  int width = driver.manage().window().getSize().getWidth();

  androidDriver.swipe( (width*9)/10, height/2, width/10, height/2, 1000);
}

public void swipeFromTo (WebElement startEl, WebElement stopEl) {
  androidDriver.swipe(startEl.getLocation().getX(), startEl.getLocation().getY(),
  stopEl.getLocation.getX(), stopEl.getLocation().getY(), 1000);
}



## Scroll
※ scrollTo(String Text), ScrollToExact(String text) 함수는 deprecated 되었으므로,  swipe 함수를 활용하길 권장함,.

puplic void scrollDown() {
  int height = driver.manage().window().getSize().getHeight();
  androidDriver.swipe(5, height * 2 / 3, 5, height / 3, 1000);
}

public void scrollUp() {
  int height = driver.manage().window().getSize().getHeight();
  androidDriver.swipe(5, height // 3, 5, height * 2 / 3, 1000);
}

public void scrollDownTo(By element) {
  int i = 0;
  while (i < 12) {
    if (driver.findElements(element).size() > 0)
      return;
    scrollDown();
    i++
  } 
  System.out.println(element.toString() + “ not found”);
}

public void scrollDownTo(String text) {
  By element = By.xpath(“//*[@text=\”” + text + “\”]”);
  androidDriver.hideKeyboard();

  int i = 0;
  while (i < 12) {
    if (androidDriver.findElements(element).size() > 0)
      return;
    scrollDown();
    i++;
  }
  System.out.println(element.toString() + “ not found”);  
}


## Orientation
androidDriver.rotate(ScreenOrientation.LANDSCAPE);

※ androidDriver.getOrientation();



## Wait
## Implicit wait
appiumDriver = new AppiumDriver(new URL(“http://0.0.0.0:4723/wd/hub”), capability);

appiumDriver.manage().timeouts().implicitlyWait(30, TimeUnit.SECONDS);


## Explicit wait
WebDriverWait wait = new WebDriverWait(appiumDriver, 10);
wait.until(ExepectedConditions.visibilityOfElementLocated(By.id(“Text”)));

※ Expected 종류
- Web element is present and clickable
- Web element is selected
- Web element is invlsible
- Selected web elment
- Presense of web element located byu
- Wait for a paricular condition
- Text present in a web element

ex)
WebDriverWait = new WebDriverWait(appiumDriver, 10);
wait.until (ExpectedConditions.visibilityofElementLocated(By.id(“Name”)));

appiumDriver.findElement(By.id(“Name”)).click();

- 추가 : https://www.browserstack.com/guide/wait-commands-in-selenium-webdriver 


##Fluent wait
Wait wait = new FluenWait (appiumDriver)
                    .withTimeout(10, TimeUnit.SECOND)
                    .pollingEvery(250, TimeUnit.MILLESECONDS)
                    .ignoring(NoSuchElementException.class)
                    .ignoring(TimeoutException.class);

wait.unitl(ExpectedConditions.visiblityOfElementLocated(By.id(“Text”)));                                           




## 스크린 저장
public void screenshot(String path_screenshot) throws IOException{
    File srcFile=driver.getScreenshotAs(OutputType.FILE);
    String filename=UUID.randomUUID().toString(); 
    File targetFile=new File(path_screenshot + filename +".jpg");
    FileUtils.copyFile(srcFile,targetFile);
}
https://medium.com/@hemanthsridhar92/enabling-video-screen-recording-for-your-appium-tests-6e0e85a1480d
http://blog.naver.com/PostView.nhn?blogId=javaking75&logNo=220549333102&parentCategoryNo=7&categoryNo=&viewDate=&isShowPopularPosts=true&from=search



기타 (링크)
- (내장/기타) 앱 실행 : https://velog.io/@dahunyoo/Execute-App 
* 이미지 활용
	- https://appium.io/docs/en/advanced-concepts/image-elements/
           - https://docs.experitest.com/display/TE/Appium+Image+Recognition 
           - https://appium.io/docs/en/writing-running-appium/image-comparison/ 
