# Selenium-Automation

package lib;

/*import org.sikuli.basics.Settings;
import org.sikuli.script.App;
import org.sikuli.script.FindFailed;
import org.sikuli.script.Key;
import org.sikuli.script.Match;
import org.sikuli.script.Region;
import org.sikuli.script.Screen;*/
import java.awt.Robot;
import java.awt.Toolkit;
import java.awt.datatransfer.StringSelection;
import java.awt.event.KeyEvent;
import java.io.BufferedInputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.net.URL;
import java.nio.charset.Charset;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.Arrays;
import java.util.Calendar;
import java.util.GregorianCalendar;
import java.util.Iterator;
import java.util.List;
import java.util.Random;
import java.util.TimeZone;
import java.util.concurrent.TimeUnit;
import java.util.logging.Level;
import java.util.logging.Logger;

import org.apache.commons.io.FileUtils;
import org.apache.pdfbox.pdfparser.PDFParser;
import org.apache.pdfbox.pdmodel.PDDocument;
import org.apache.pdfbox.util.PDFTextStripper;
import org.apache.poi.xssf.usermodel.XSSFSheet;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.JavascriptExecutor;
import org.openqa.selenium.Keys;
import org.openqa.selenium.OutputType;
import org.openqa.selenium.TakesScreenshot;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.server.browserlaunchers.Sleeper;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.WebDriverWait;
/*import javax.mail.MessagingException;
import javax.mail.internet.AddressException;*/
//import org.apache.derby.client.am.DateTime;
/*import util.DbManager;
import util.SikuliLib;*/
/*import util.TestUtil;

import util.TableContentsContainer;
import util.Table;*/
/*import util.AutomationException;
import util.OAM;
import lib.UtilityFun;*/
//import org.joda.time.DateTime;
//import org.joda.time.DateTimeZone;
//import com.sun.jna.platform.FileUtils;
import org.testng.Assert;




/**
 * @author Abox8
 *
 */
/**
 * @author Abox8
 *
 */
public class KeywordsApp extends DriverApp {	
	public static Random randomGenerator = new Random();
	public static Calendar cal = new GregorianCalendar();  //used for adding current date in variable and then used in paths
	public static int date = cal.get(Calendar.DATE);  //used for adding current date in variable and then used in paths
	public static int month = cal.get(Calendar.MONTH);  //used for adding current date in variable and then used in paths
	public static int year = cal.get(Calendar.YEAR);  //used for adding current date in variable and then used in paths
	public static int sec =cal.get(Calendar.SECOND);  //used for adding current date in variable and then used in paths
	public static int day =cal.get(Calendar.HOUR_OF_DAY);  //used for adding current date in variable and then used in paths
	public static int hour=cal.get(Calendar.HOUR);  //used for adding current date in variable and then used in paths
	public static int min=cal.get(Calendar.MINUTE);  //used for adding current date in variable and then used in paths
	public static String sMin = new Integer(randomGenerator.nextInt(60)).toString(); //Converted Integer value to String and then used in paths
	public static String sSec=new Integer(randomGenerator.nextInt(60)).toString(); //Converted Integer value to String and then used in paths
	public static String sHour=new Integer(randomGenerator.nextInt(24)).toString();  //Converted Integer value to String and then used in paths
	public static String sDate=new Integer(date).toString();  //Converted Integer value to String and then used in paths
	public static String call_id ; //Used in GetText() and DBQuerycheck() to store the call id to be used for UI
	public static String sUser=null;
	public static String sUser_Name;
	public static Xlfile_Reader datareader=null; //Initialize the Xlfilereader excel file
	public static Xlfile_Reader datawriter=null; //Initialize the Xlfilereader excel file
	public static float round;
	public static float round1;
	public static WebDriverWait wait;
	public static String script_error=null;
	public static int globalwait;
	public static String winHandleBefore;
	public static String dateFrom;
	public static String dateTo;
	public static String poc;
	public static String timeZoneDefault;
	public static String sessionID;
	public static String text;
	public static String text1;
	public static String val;
	public static int rc;
	public static float sum;
	public static int  payable1;
	public static  int i=0;
	public static int index=1;
	public static int TP_final_Value;
	

	public static String Ecovernote;
	private final static Logger logger = Logger.getLogger(TestReports.class.getName());
	
	public static String navigateTo(){
		try{
			driver.navigate().to(CONFIG.getProperty("testUrl"));
			File scrFile = ((TakesScreenshot)driver).getScreenshotAs(OutputType.FILE);
	        FileUtils.copyFile(scrFile, new File("D:\\Automation\\Screenshots\\1.png"));
	              
						return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	public static String Login(){
		try{
			driver.navigate().to(CONFIG.getProperty("testUrl"));
			if (driver.getTitle().equalsIgnoreCase(CONFIG.getProperty("Title")))
			{
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(Objects.getProperty(object));
			
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(CONFIG.getProperty("Username"))));
				WebElement username = driver.findElement(By.xpath(CONFIG.getProperty("Username")));
				WebElement password = driver.findElement(By.xpath(CONFIG.getProperty("Password")));
				username.sendKeys(CONFIG.getProperty("testUsername"));
		     	username.sendKeys(Keys.TAB);
		     	password.sendKeys(CONFIG.getProperty("testPassword"));
		     	WebElement btnclick = driver.findElement(By.xpath(CONFIG.getProperty("Signin")));
		     	btnclick.click();
			}
						return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	public static String navigateToCustomer(){
		try{
			JavascriptExecutor jscript = (JavascriptExecutor) driver; 
			jscript.executeScript("window.open()");
			for(String winHandle :driver.getWindowHandles()){
                driver.switchTo().window(winHandle);
                
			}
			driver.navigate().to(CONFIG.getProperty("Customer_URL"));
			return PASS;
		
		}
			catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	public static String waitSometime(){
		try{
			Thread.sleep(1000);
			return PASS;
		
		}
			catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	public static String navigateToAgent(){
		try{
			//driver.navigate().to(Objects.getProperty(object));
			
			//driver.findElement(By.cssSelector("body")).sendKeys(Keys.CONTROL +"t");
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			
                
			//driver.navigate().to("http://148.147.167.217:8888/acs/client/main/demo/firstbank.html");
			
			driver.navigate().to(CONFIG.getProperty("Agent_URL"));
			return PASS;
		
		}
			catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	public static String RightClicknOpenLinkinTab()
	{
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.presenceOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			Actions builder=new Actions(driver);
			
			builder.contextClick(link).perform();
			
			driver.findElement(By.cssSelector("body")).sendKeys(Keys.CONTROL +"t");
			
			return PASS;
		}
		catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
		
	}

public static String getAgentSessionID()
{
	try
	{
		logger.log(Level.INFO,"Executing keyword: " + keyword);
	
	driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
    wait.until(ExpectedConditions.elementToBeClickable(By.xpath(Objects.getProperty(object))));
	WebElement CreateID = driver.findElement(By.xpath(Objects.getProperty(object)));
	
	sessionID=CreateID.getText();
	System.out.println(sessionID);
	return PASS;
	}
	catch(Throwable t)
	{
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
	
}


public static String putAgentSessionID()
{
	try
	{
		
		logger.log(Level.INFO,"Executing keyword: " + keyword);
	driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
    wait.until(ExpectedConditions.elementToBeClickable(By.xpath(Objects.getProperty(object))));
	WebElement JoinID = driver.findElement(By.xpath(Objects.getProperty(object)));
	
	JoinID.sendKeys(sessionID.trim());
	
	return PASS;
	}
	catch(Throwable t)
	{
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
	
	
}
	public static String clickDialog()
	{
		try
		{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
//			wait = new WebDriverWait(driver, 30);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			String expectedString = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(expectedString);
			/*SikuliLib.OpenFile(expectedString);*/
			return PASS;
		}
		catch(Throwable t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	
	public static String clickLink(){
		try{
		
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			
			waitSometime();
			link.click();
			
			
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	
	public static String clickselector(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector(Objects.getProperty(object))));
			
			
			WebElement link = driver.findElement(By.cssSelector(Objects.getProperty(object)));
			link.click();
			
			
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	
	
	
	
	public static String clickLinkSubmit(){
		try{
			
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			link.submit();
			
						
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	public static String uploadFile(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(data);
			
			StringSelection sel = new StringSelection(data);
			Toolkit.getDefaultToolkit().getSystemClipboard().setContents(sel,null);
			 System.out.println("selection" +data);
			 Robot robot = new Robot();
			      
			  // Press Enter
			 robot.keyPress(KeyEvent.VK_ENTER);
			 
			// Release Enter
			 robot.keyRelease(KeyEvent.VK_ENTER);
			 
			  // Press CTRL+V
			 robot.keyPress(KeyEvent.VK_CONTROL);
			 robot.keyPress(KeyEvent.VK_V);
			 
			// Release CTRL+V
			 robot.keyRelease(KeyEvent.VK_CONTROL);
			 robot.keyRelease(KeyEvent.VK_V);
			 ////Thread.sleep(1000);
			        
			       
			 robot.keyPress(KeyEvent.VK_ENTER);
			 robot.keyRelease(KeyEvent.VK_ENTER);
			
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	public static String clickNext(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			link.click();
			
			
			
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	public static String clickImage(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			link.click();
			
			
			
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	public static String clickOnLookup(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			
			waitSometime();
			link.click();
			
			
			
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	public static String clickOnLookupxpath(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			link.click();
			
			
			
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	public static String selectFromDate(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			if(CommonData.containsKey(data)){
				data = CommonData.getProperty(data);
				
			}
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			link.click();
			 wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty("CFA_Year"))));
			WebElement year = driver.findElement(By.xpath(Objects.getProperty("CFA_Year")));
			
			year.click();
			year.click();
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty("CFA_Date_OK"))));
			WebElement CalendarOK = driver.findElement(By.xpath(Objects.getProperty("CFA_Date_OK")));
			CalendarOK.click();
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	public static String mouseClick(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
	        Actions builder = new Actions(driver);    
	        builder.moveToElement(link).click(link);    
	        builder.perform(); 
	        return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	public static String mouseHover(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
	        Actions builder = new Actions(driver);    
	        builder.moveToElement(link).perform();
	        return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	
	public static String closeBrowser(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			//WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			//driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	       // wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
	        //Actions builder = new Actions(driver);    
	        //builder.moveToElement(link).perform();
			////Thread.sleep(1000);
				driver.close();
				driver.switchTo().window(winHandleBefore);
	        return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	public static String textLink(){
        try{
               logger.log(Level.INFO,"Executing keyword: " + keyword);
               WebElement link = driver.findElement(By.linkText(Objects.getProperty(object)));
               driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
         //wait.until(ExpectedConditions.visibilityOfElementLocated(By.linkText(Objects.getProperty(object))));
               wait.until(ExpectedConditions.presenceOfElementLocated(By.linkText(Objects.getProperty(object))));
               link.click();
               
               /*String certificate = CONFIG.getProperty("CertificateErr");*/
               /*Screen scr = new Screen();
               if (scr.exists(certificate) != null){
                     SikuliLib.clickImage(certificate);
                     ////Thread.sleep(5000);
                     scr.type(Key.DOWN);
                     scr.type(Key.ENTER);
                     scr.mouseMove(scr.getCenter());
                     //Thread.sleep(20000);
               }*/
               return PASS;
        }catch(Throwable t){
               logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
               return FAIL;
        }
 }



	public static String getWindowHandleBefore()
	{
		try
		{
			/*winHandleBefore = driver.getWindowHandle();
			System.out.println(winHandleBefore);
			System.out.println(driver.getTitle());*/
			////Thread.sleep(3000);
			driver.switchTo().window(winHandleBefore);
			System.out.println(driver.getTitle());
			return PASS;
		}
		catch(Exception e)
		{
			return FAIL;
		}
	}
	
	
	public static String SwitchToAlert()
	{
		try
		{
         Alert alert = driver.switchTo().alert();
          alert.accept();
             return PASS;

		
			
		}
		catch(Exception e)
		{
			return FAIL;
		}
	}
	
	public static String switchToTab(){
		try{
			Actions newTab = new Actions(driver);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			while(true)
			{
			newTab.sendKeys(Keys.chord(Keys.CONTROL,Keys.TAB)).perform();
			if(driver.getTitle().contains(data))
			{
				break;
			}
			}
			 //newTab.remove(winHandleBefore);
			    // change focus to new tab
			 //System.out.println(newTab);
			   // driver.switchTo().window(newTab.get(0));
		   
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	public static String switchToNewWindow(){
		try{
			/*if (CONFIG.getProperty("testBrowser").equalsIgnoreCase("*iexplore"))
			{
				
				driver.get("javascript:document.getElementById('overridelink').click();");
			}*/
			winHandleBefore = driver.getWindowHandle();
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			WebDriver popup = null;
		    Iterator<String> windowIterator = driver.getWindowHandles().iterator();
		    
		    while(windowIterator.hasNext())
		    { 
		    	String windowHandle = windowIterator.next(); 
		    	System.out.println(windowHandle);
		    	popup = driver.switchTo().window(windowHandle);
		    	System.out.println(popup.getTitle());
		    	/*if (popup.getTitle().contains(data))
		    	{
		    		System.out.println(popup.getTitle());
		    		break;
		    	}*/
		    }
		    
		   
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
		
	public static String select(){
		try{
			WebElement sel=null;
			
			waitSometime();
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			// If value is a key, the real value will be getting from Property file
			/*if(CommonData.containsKey(data)){
				data = CommonData.getProperty(data);
			}*/
			
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.or(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))), 
					ExpectedConditions.visibilityOfElementLocated(By.cssSelector(Objects.getProperty(object))),
					ExpectedConditions.visibilityOfElementLocated(By.name(Objects.getProperty(object)))));
			if (driver.findElements(By.xpath(Objects.getProperty(object))).size() > 0)
			{
				sel = driver.findElement(By.xpath(Objects.getProperty(object)));
			}
			else if (driver.findElements(By.cssSelector(Objects.getProperty(object))).size() > 0)
			{
				sel = driver.findElement(By.cssSelector(Objects.getProperty(object)));
			}
			else
			{
				sel = driver.findElement(By.name(Objects.getProperty(object)));
			}
			
			List<WebElement> options= sel.findElements(By.tagName("option"));
			System.out.println(options);
			for (WebElement option: options)
			{
				if(data.equals(option.getText()))
				{
					Sleeper.sleepTight(200);
					option.click();
					break;
				}
			}
			
			/*Select droplist = new Select(driver.findElement(By.xpath(Objects.getProperty(object))));   
			System.out.println(droplist.getOptions());
			droplist.selectByVisibleText(data);
			//Thread.sleep(20000);*/
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Not Found " + tsData);
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}


	public static String selectAll(){
		try{
			
			////Thread.sleep(3000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			// If value is a key, the real value will be getting from Property file
			/*if(CommonData.containsKey(data)){
				data = CommonData.getProperty(data);
			}*/
			
			WebElement sel = driver.findElement(By.xpath(Objects.getProperty(object)));
			List<WebElement> options= sel.findElements(By.tagName("option"));
			//options.clear();
			
			for (WebElement option: options)
			{
				
					option.click();
					
				
			}
			
			/*Select droplist = new Select(driver.findElement(By.xpath(Objects.getProperty(object))));   
			System.out.println(droplist.getOptions());
			droplist.selectByVisibleText(data);
			//Thread.sleep(20000);*/
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	public static String switchToDefaultContent()
	{
		try
		{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			//String data = testData.getCellData(currentFTID, tsData, currentTCID);
			driver.switchTo().defaultContent();
			return PASS;
		}
		//
		catch(Throwable t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
			
	}
	
	
	

	public static String waitfor(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			float test = (Float.parseFloat(data));
			int test1 = (int) test;
			//Thread.sleep(test1);
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	/**
	 * Input value for text box
	 * @param param1 - The value that need to fill into text box
	 * @return Pass or Fail
	 */
	public static String input(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			//System.out.println(Objects.getProperty(object));
			System.out.println(data);
			
		//	////Thread.sleep(1000);
				wait = new WebDriverWait(driver, 60);
//			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
				WebElement entertext = driver.findElement(By.xpath(Objects.getProperty(object)));
				entertext.clear();
		        entertext.sendKeys(data);
		     	entertext.sendKeys(Keys.TAB);
		
			
	        return PASS;
		}catch(Exception t){	
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	/*
	public static String input1(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			//System.out.println(Objects.getProperty(object));
			System.out.println(data);
			
		//	////Thread.sleep(1000);
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector(Objects.getProperty(object))));
				WebElement entertext = driver.findElement(By.cssSelector(Objects.getProperty(object)));
				entertext.clear();
		        entertext.sendKeys(data);
		     	entertext.sendKeys(Keys.TAB);
		
			
	        return PASS;
		}catch(Exception t){	
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}*/
	
	public static String SelectProduct(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(Objects.getProperty(object));
			
			//Thread.sleep(2000);
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
				WebElement entertext = driver.findElement(By.xpath(Objects.getProperty(object)));
				entertext.clear();
		        entertext.sendKeys(data);
		     	entertext.sendKeys(Keys.ARROW_DOWN);
		     	entertext.sendKeys(Keys.ENTER);
		     	////Thread.sleep(1000);
				driver.findElement(By.id("inwardDate")).click();
				driver.findElement(By.id("inwardDate")).click();
				driver.findElement(By.linkText("1")).click();
				////Thread.sleep(1000);			
		     	
			
	        return PASS;
		}catch(Exception t){	
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	public static String ADate(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(Objects.getProperty(object));
			System.out.println(data);
			
			////Thread.sleep(1000);
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.name(Objects.getProperty(object))));
				WebElement entertext = driver.findElement(By.name(Objects.getProperty(object)));
				entertext.clear();
		        entertext.sendKeys(data);
		        ////Thread.sleep(1000);
		     	entertext.sendKeys(Keys.TAB);
		
			
	        return PASS;
		}catch(Exception t){	
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	public static String SelectDate(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(Objects.getProperty(object));
			System.out.println(data);
			
			////Thread.sleep(1000);
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
				WebElement entertext = driver.findElement(By.xpath(Objects.getProperty(object)));
				entertext.clear();
		        entertext.sendKeys(data);
				//entertext.click();
		        ////Thread.sleep(1000);
		        entertext.sendKeys(Keys.TAB);
		
			
	        return PASS;
		}catch(Exception t){	
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	/*public static String SelectregDate(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			//System.out.println(Objects.getProperty(object));
			System.out.println(data);
			
			////Thread.sleep(1000);
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//form/table/tbody/tr")));
				List<WebElement> row1 = driver.findElements(By.xpath("//form/table/tbody/tr"));
				System.out.println("Row Size is "+row1.size());
				int j=1;
				List<WebElement> col1 = driver.findElements(By.xpath("//form/table/tbody/tr/td["+j+"]"));
				System.out.println("Col Size is "+col1.size());
				
				for(int i=4;i<row1.size(); i++)
				{
					for(j=1;j<col1.size(); j++)
					{	
					  WebElement cal=driver.findElement(By.xpath("//form/table/tbody/tr["+ i +"]/td[" +j +"]"));
					  System.out.println(cal.getText());					  
					  
					  if(data.equalsIgnoreCase(cal.getText()))
					  {
						  cal.click();
						//  System.out.println("veeru");
						  break;
						  
					 }
				}}
				
//				entertext.clear();
//		        entertext.sendKeys(data);
//		        ////Thread.sleep(1000);
//		     	entertext.sendKeys(Keys.TAB);
		
			
	        return PASS;
		}catch(Exception t){	
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}*/
	
	
	
	public static String SelectregDate(){
        try{
               logger.log(Level.INFO,"Executing keyword: " + keyword);
               // Value is getting from excel file
               //String data = testData.getCellData(currentFTID, tsData, currentTCID);
               //System.out.println(Objects.getProperty(object));
               //System.out.println(data);
               
               waitSometime();
               Calendar c =Calendar.getInstance(TimeZone.getDefault());
               //Get current date
               int todayInt=c.get(Calendar.DAY_OF_MONTH);
               //Integer to String
               String today = Integer.toString(todayInt);
               ////Thread.sleep(1000);
                     driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
                      wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//form/table/tbody/tr")));
                     List<WebElement> row1 = driver.findElements(By.xpath("//form/table/tbody/tr"));
                     System.out.println("Row Size is "+row1.size());
                     int i=4;
                     int j=1;
                     List<WebElement> col1 = driver.findElements(By.xpath("//form/table/tbody/tr["+i+"]/td"));
                     System.out.println("Col Size is "+col1.size());
                     boolean breakLoop = false;
                     myloop:       for(i=4;i<=row1.size(); i++)
                     {
                     
                            for(j=1;j<col1.size(); j++)
                                   
                            {      
                                   
                              WebElement cal=driver.findElement(By.xpath("//form/table/tbody/tr["+ i +"]/td[" +j +"]"));
                              System.out.println(cal.getText());                                   
                              
                              if(today.equalsIgnoreCase(cal.getText()))
                              {      
                            	     
                            	     waitSometime();
                              
                                     cal.click();
                                   //  System.out.println("veeru");
                                     
                                     break myloop;
                                     
                             
                     }}
                     }
                     
                     
                     
                     
                     
                 	return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	
	
	
	
	
	public static String getBatchIDPolNum()
	{
		try{
			//Thread.sleep(2000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			////Thread.sleep(1000);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			
			WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
			text = element.getText();
			System.out.println("text= " + text);
			WritePolicyNumber(text);
			
			return PASS;
			}catch(Exception t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	public static String  WritePolicyNumber(String text)
	{
		try{
			//Thread.sleep(2000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			////Thread.sleep(1000);
			

			File src= new File("D:\\RSA-Automation\\vamautomationeMotor\\src\\test\\java\\Results\\PolicyNumber.xlsx");
			

				
			 FileInputStream fis=new FileInputStream(src);
		
			 XSSFWorkbook wb=new XSSFWorkbook(fis);
			 System.out.println("file loaded");
             XSSFSheet sh1=wb.getSheet("Sheet1");
			
             int i=0;
             while(true){
            	 
            	if(sh1.getRow(i).getCell(0)!=null){
            		i++;
            	}else{
            		break;
            	} 
             }
             sh1.createRow(i).createCell(0).setCellValue(text);
             //row.createCell(lastrow).setCellValue("Appending in the end");
             
             
         
			 FileOutputStream fos=new FileOutputStream("D:\\RSA-Automation\\vamautomationeMotor\\src\\test\\java\\Result\\PolicyNumber\\PolicyNumber.xlsx");
			 
			
			 
			 wb.write(fos);
			 fos.close();
			 
	
		 return PASS;
		}
		
		
		catch(Exception t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	
	}
	
	
	
	
	
	public static String getBatchval()
	{
		try{
			//Thread.sleep(2000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
			text = element.getAttribute("value");
			System.out.println("text= " + text);
			
			return PASS;
			}catch(Exception t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}

	
	public static String selectquote1()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
			text=text.replaceAll(",", "");
			//text=text.substring(0,text.indexOf("."));
			element.sendKeys(text);
			WebElement elem=driver.findElement(By.xpath(Objects.getProperty(object)));
			elem.click();
			WebElement elem1=driver.findElement(By.xpath("table[2]/tbody/tr/td[1]/fieldset/form/div"));
			String msg=elem1.getText();
			if(!msg.contains("No Messages Found!"))
			
				  driver.findElement(By.xpath("table[2]/tbody/tr[1]/td[1]/fieldset/form/table/tbody/tr[2]/td[3]/a")).click();
		
			else
			{
				driver.findElement(By.xpath("form/table[2]/tbody/tr[2]/td[9]/a/img")).click();
			    ////Thread.sleep(1000);
			    driver.findElement(By.xpath("//table[2]/tbody/tr/td[1]/div/ul/li[2]/a")).click();
		        ////Thread.sleep(1000);
				driver.findElement(By.xpath("table[2]/tbody/tr[1]/td[1]/fieldset/form/table/tbody/tr[2]/td[3]/a")).click();
			}	
			
			return PASS;
			
			}catch(Exception t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	public static String selectquote()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);  
					
       try{			
			WebElement elem1=driver.findElement(By.xpath("//table[2]/tbody/tr/td[1]/fieldset/form/div"));
			String msg=elem1.getText();
			System.out.println("message is "+msg);
			driver.findElement(By.xpath("//form/table[2]/tbody/tr[2]/td[9]/a/img")).click();
		    ////Thread.sleep(1000);
		    driver.findElement(By.xpath("//table[2]/tbody/tr/td[1]/div/ul/li[2]/a")).click();
	        ////Thread.sleep(1000);
			driver.findElement(By.xpath("//table[2]/tbody/tr[1]/td[1]/fieldset/form/table/tbody/tr[2]/td[3]/a")).click();
       }
       
       catch(Exception t){
			
    	   driver.findElement(By.xpath("//table[2]/tbody/tr[1]/td[1]/fieldset/form/table/tbody/tr[2]/td[3]/a")).click();
       }
		
			
			
			return PASS;
			
			}catch(Exception t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	
	/*public static String selectRP()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			List<WebElement> element1=driver.findElements(By.xpath("//form/table/tbody/tr[1]/td/fieldset/table/tbody/tr"));
			System.out.println("size is .."+element1.size());
		

			//List<WebElement> element1=driver.findElements(By.xpath(""));
			//System.out.println("size is .."+element1.size());
			
			//form/table/tbody/tr[1]/td/fieldset/table//
			for(int i=0;i<element1.size(); i++)
			{
				
				WebElement element=driver.findElement(By.xpath("//form/table/tbody/tr[1]/td/fieldset/table/tbody/tr["+ i +"]/td[2]"));
				text=element.getText();
				System.out.println("Policy no is"+text);
				if(!text.endsWith("0") )
				{
					driver.findElement(By.xpath("//form/table/tbody/tr[1]/td/fieldset/table/tbody/tr["+i+"]/td[1]")).click();
				    break;
					
				}	
				}
			
			
			return PASS;
		}
		catch(Exception t)
		{
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
		*/
	public static String selectRP()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			//List<WebElement> element1=driver.findElements(By.xpath(".//*[@id='renewalfrm']/table/tbody/tr[1]/td/fieldset/table"));
			
			List<WebElement> element1=driver.findElements(By.xpath("//input[@name='policyId']"));
	
			System.out.println("size is .."+element1.size());
		

						
			//count the number  of element policy number
			for(int i=8;i<element1.size(); i++)
			{
				
				//WebElement element=driver.findElement(By.xpath("//form/table/tbody/tr[1]/td/fieldset/table/tbody/tr["+ i +"]/td[1]"));
				WebElement element=driver.findElement(By.xpath(".//*[@id='renewalfrm']/table/tbody/tr[1]/td/fieldset/table/tbody/tr[" + i +"]/td[2]"));
				
			
				
				
				//text=element.getText();
				System.out.println("Policy no is"+text);
			
				if(!text.endsWith("0") )
				{
					driver.findElement(By.xpath(".//*[@id='renewalfrm']/table/tbody/tr[1]/td/fieldset/table/tbody/tr[" + i +"]/td[2]")).click();
				    //Sleeper.sleepTightInSeconds(20);
					break;
					
				}	
				}
			
			
			return PASS;
		}
		catch(Exception t)
		{
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
		}
		}
	public static String selectReceipt()
	{
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			
			List<WebElement> elementr=driver.findElements(By.xpath("//form/table[2]/tbody/tr/td/fieldset/table/tbody/tr"));
			System.out.println("size is .."+elementr.size());   
			WebElement p1=driver.findElement(By.xpath("//form/table[1]/tbody/tr[2]/td/fieldset/table/tbody/tr[6]/td[5]")); 
			String strp=p1.getText();
			strp=strp.replaceAll(",","");
			System.out.println("value is .."+strp);
			//form/table/tbody/tr[1]/td/fieldset/table//
			for(int i=2;i<elementr.size(); i++)
			{
				
				WebElement elementp=driver.findElement(By.xpath("//form/table[2]/tbody/tr/td/fieldset/table/tbody/tr["+ i +"]/td[2]"));
				 text1=elementp.getText();
				System.out.println("Receipt no is"+text1);
				if(text.equalsIgnoreCase(text1) )
				{
					driver.findElement(By.xpath("//form/table[2]/tbody/tr/td/fieldset/table/tbody/tr["+i+"]/td[1]")).click();
					//Thread.sleep(2000);
				
					WebElement entertext = driver.findElement(By.xpath("//form/table[2]/tbody/tr/td/fieldset/table/tbody/tr["+i+"]/td[6]/input"));
								
					////Thread.sleep(5000);
			        entertext.sendKeys(strp);			
					
				    break;
					
				}	
				}
			
			
			return PASS;
		}
		catch(Exception t)
		{
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	
	public static String selectBranchcode()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			
			System.out.println("Data is..." +data);
			
			
			////Thread.sleep(1000);
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
				List<WebElement> entertext = driver.findElements(By.xpath(Objects.getProperty(object)));
				/*entertext.clear();
		        entertext.sendKeys(data);
		        ////Thread.sleep(1000);
		     	entertext.sendKeys(Keys.TAB);*/
			System.out.println("size is .."+entertext.size());
		
			//form/table/tbody/tr[1]/td/fieldset/table//
			for(int i=2;i<entertext.size(); i+=2)
			{
				
				WebElement element3=driver.findElement(By.xpath("//form/table/tbody/tr["+ i +"]/td[2]"));
						
						
						//entertext+"["+ i +"][/td[2]]"));
				text=element3.getText();
				System.out.println("code is"+text);
				if(text.equalsIgnoreCase(data) )
				{
					driver.findElement(By.xpath("//form/table/tbody/tr["+ i +"]/td[1]")).click();
							
							//  "//entertext+["+ i +"]/td[1]")).click();
				    break;
					
				}	
				}
			
			
			return PASS;
		}
		catch(Exception t)
		{
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	
	public static String putBatchval()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
			text=text.replaceAll(",", "");
			text=text.substring(0,text.indexOf("."));
			element.sendKeys(text);
			System.out.println("text= " + text);
			return PASS;
			}catch(Exception t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	
	public static String putBatchmultipay()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
			text=text.replaceAll(",", "");
			//text=text.substring(0,text.indexOf("."));
			int x=(int)Math.ceil(Double.parseDouble(text)/2);
			String y;
			if(x<50000)
			{
				y=Integer.toString(x);
			}
			else
			{
				y= Integer.toString(x/2);
			}
			
			element.sendKeys(y);
			System.out.println("text= " + y);
			return PASS;
			}catch(Exception t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	
	public static String putBatchIDV()
	{
		try{
			////Thread.sleep(1000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
			text=text.replaceAll(",", "");
			//text=text.substring(0,text.indexOf("."));
			int x=(int)Math.ceil(Double.parseDouble(text)*31/100);
			 System.out.println(x);
			 x=(int)Math.ceil(Double.parseDouble(text)+x);
			 String y=Integer.toString(x);
			    element.clear();
			    ////Thread.sleep(1000);
				element.sendKeys(y);
			System.out.println("text= " + y);
			return PASS;
			}catch(Exception t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
	
//	public static String getValue(){
//		try{
//			logger.log(Level.INFO,"Executing keyword: " + keyword);
//			// Value is getting from excel file
//			String data = testData.getCellData(currentFTID, tsData, currentTCID);
//			System.out.println(Objects.getProperty(object));
//			System.out.println(data);
//			
//			/*//Thread.sleep(2000);*/
//				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
//				wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
//				
//				WebElement Value = driver.findElement(By.xpath(Objects.getProperty(object)));
//				String Amount=Value.getText();
//				//System.out.println("Amount is "+Value.getText());
//				
//		     	Value.sendKeys(Keys.TAB);
//		     	WebElement Amount1 = driver.findElement(By.xpath("//form/table[2]/tbody/tr/td/fieldset/table/tbody/tr[2]/td[2]/input[1]"));
//		     	String val=Amount1.replaceAll(",","");
//		     	Amount1.sendKeys(val);
//		     	System.out.println(val);
//		     	
//	        return PASS;
//		}catch(Exception t){	
//			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
//			return FAIL;
//		}
//	}
	
	
	
	public static String inputbyname(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			// Value is getting from excel file
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(Objects.getProperty(object));			
			
				driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
				wait.until(ExpectedConditions.visibilityOfElementLocated(By.name(Objects.getProperty(object))));
				WebElement entertext = driver.findElement(By.name(Objects.getProperty(object)));
				entertext.clear();
		       entertext.sendKeys(data);    
		       entertext.sendKeys(Keys.ARROW_DOWN);
		       entertext.sendKeys(Keys.TAB);
			
	       return PASS;
		}catch(Exception t){	
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}


	/* @FindBy(id="name")
	 public static WebElement AgentName;   // Agent Name


	    @FindBy(id="avCreateBtn")
	    public static WebElement CreateSession1;	*/

	
	/**
	 * @description: select value in dropdown
	 * @param 	data - value to select
	 * @return Pass or Fail
	 * @author parvez
	 * @Date	14/01/2015
	 */
//	public static String select(){
//		try{
//			logger.log(Level.INFO,"Executing keyword: " + keyword);
//			String data = testData.getCellData(currentFTID, tsData, currentTCID);
//			// If value is a key, the real value will be getting from Property file
//			/*if(CommonData.containsKey(data)){
//				data = CommonData.getProperty(data);
//			}*/
//			/*switchToFrame();*/
//			////Thread.sleep(3000);
//			System.out.println(data);
//			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
//			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
//			WebElement sel = driver.findElement(By.xpath(Objects.getProperty(object)));
//			List<WebElement> options= sel.findElements(By.tagName("option"));
//			/*options.clear();*/
//			System.out.println(options);
//			for (WebElement option: options)
//			{
//				if(data.equals(option.getText()))
//				{
//					System.out.println(option.getText());
//					option.click();
//					break;
	
	
//				}
//			}
//			//Thread.sleep(2000);
//			/*Select droplist = new Select(driver.findElement(By.xpath(Objects.getProperty(object))));   
//			System.out.println(droplist.getOptions());
//			droplist.selectByVisibleText(data);
//			//Thread.sleep(20000);*/
//			return PASS;
//		}catch(Throwable t){
//			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
//			return FAIL;
//		}
//	}
	public static String selectbyname(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			// If value is a key, the real value will be getting from Property file
			/*if(CommonData.containsKey(data)){
				data = CommonData.getProperty(data);
			}*/
			/*switchToFrame();*/
			////Thread.sleep(5000);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.name(Objects.getProperty(object))));
			WebElement sel = driver.findElement(By.name(Objects.getProperty(object)));
			List<WebElement> options= sel.findElements(By.tagName("option"));
			/*options.clear();*/
			System.out.println(options);
			for (WebElement option: options)
			{
				if(data.equals(option.getText()))
				{
					System.out.println(option.getText());
					option.click();
					break;
				}
			}
			//Thread.sleep(2000);
			/*Select droplist = new Select(driver.findElement(By.xpath(Objects.getProperty(object))));   
			System.out.println(droplist.getOptions());
			droplist.selectByVisibleText(data);
			//Thread.sleep(20000);*/
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	/**
	 * Description: Swtich to the IFrame of CoBrowsing Agent screen 
	 * Param: verify value in the dropdown
	 * @return: Pass or Fail
	 * author: Parvez
	 * date: 15/01/2015
	 */
	public static String selectbyCSS(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			// If value is a key, the real value will be getting from Property file
			/*if(CommonData.containsKey(data)){
				data = CommonData.getProperty(data);
			}*/
			/*switchToFrame();*/
			////Thread.sleep(5000);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.cssSelector(Objects.getProperty(object))));
			WebElement sel = driver.findElement(By.cssSelector(Objects.getProperty(object)));
			List<WebElement> options= sel.findElements(By.tagName("option"));
			/*options.clear();*/
			System.out.println(options);
			for (WebElement option: options)
			{
				if(data.equals(option.getText()))
				{
					System.out.println(option.getText());
					option.click();
					break;
				}
			}
			//Thread.sleep(2000);
			/*Select droplist = new Select(driver.findElement(By.xpath(Objects.getProperty(object))));   
			System.out.println(droplist.getOptions());
			droplist.selectByVisibleText(data);
			//Thread.sleep(20000);*/
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	public static void switchToFrame()
	{
		try
		{
			////Thread.sleep(10000);
//			wait = new WebDriverWait(driver, 20);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			
			
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//iframe")));
			List<WebElement> frames = driver.findElements(By.xpath("//iframe"));
			
			System.out.println("Total Frames : " + frames.size());
			for (WebElement frame : frames)
			{
			System.out.println("Frame Details : id : " + frame.getAttribute("id")
			+ " SRC : " + frame.getAttribute("src") + "index:" + frame.getAttribute("index"));
			String childurl=frame.getAttribute("src");
			}
			////Thread.sleep(10000);
			if (frames.size()!=0)
			{
			driver.switchTo().frame(driver.findElement(By.xpath("//iframe[contains(@src,'view.html')]")));
			}
			
		}
		catch(Throwable t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			
		}
	}
	
	/**
	 * @description: select value in dropdown
	 * @param 	data - value to select
	 * @return Pass or Fail
	 * @author Parvez
	 * @Date	Mar-11-2014
	 */
	public static String VerifyDropdownValue(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			switchToFrame();
			String value = FAIL;
//			wait = new WebDriverWait(driver, 30);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.id(Objects.getProperty(object))));
			WebElement sel = driver.findElement(By.id(Objects.getProperty(object)));
			List<WebElement> options= sel.findElements(By.tagName("option"));
			
			for (WebElement option: options)
			{
				if(data.equals(option.getText()))
				{
					value=PASS;
					System.out.println(option.getText());
					break;
					
				}
			}
			return value;
			}
		
		
			catch(Throwable t)
			{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
		
		
	}
	
	
	/**
	 * @description: VerifyEnteredTextValue
	 * @param 	data - value to verify
	 * @return Pass or Fail
	 * @author Parvez
	 * @Date	Mar-11-2014
	 */
	public static String VerifyEnteredTextValue(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			switchToFrame();
			String value = FAIL;
			//Thread.sleep(20000);
//			wait = new WebDriverWait(driver, 120);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.id(Objects.getProperty(object))));
			WebElement input = driver.findElement(By.id(Objects.getProperty(object)));
			System.out.println(input.getAttribute("value"));
			if (data.equals(input.getAttribute("value")))
					{
				System.out.println(input.getAttribute("value"));
				value=PASS;
					}
			return value;
		}
			catch(Throwable t)
			{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
		
		
	}
	
	
	/**
	 * @description: VerifyCheckboxIsSet
	 * @param 	data - value to verify
	 * @return Pass or Fail
	 * @author Parvez
	 * @Date	Mar-11-2014
	 */
	public static String VerifyCheckboxIsSet(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			switchToFrame();
			String value = FAIL;
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.id(Objects.getProperty(object))));
			WebElement check = driver.findElement(By.id(Objects.getProperty(object)));
			
			System.out.println(check.getAttribute("value"));
			if (check.isSelected())
					{
						value=PASS;
					}
			
			return value;
		}
			catch(Throwable t)
			{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
		
		
	}
	
	/**
	 * @description: VerifyCheckboxIsNotSet
	 * @param 	data - value to verify
	 * @return Pass or Fail
	 * @author Parvez
	 * @Date	Mar-11-2014
	 */
	public static String VerifyCheckboxIsNotSet(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			switchToFrame();
			String value = FAIL;
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.id(Objects.getProperty(object))));
			WebElement check = driver.findElement(By.id(Objects.getProperty(object)));
			
			System.out.println(check.getAttribute("checked"));
			if (!check.getAttribute("checked").contains("checked"))
					{
						value=PASS;
					}
			
			return value;
		}
			catch(Throwable t)
			{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
		
		
	}
	
	
	/**
	 * @description: VerifyRadioButtonIsSet
	 * @param 	data - value to verify
	 * @return Pass or Fail
	 * @author Parvez
	 * 
	 * 
	 * 
	 * @Date	Mar-11-2014
	 */
	public static String VerifyRadioButtonIsSet(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			switchToFrame();
			String value = FAIL;
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.id(Objects.getProperty(object))));
			WebElement check = driver.findElement(By.id(Objects.getProperty(object)));
			
			System.out.println(check.getAttribute("value"));
			if (check.isSelected())
					{
						value=PASS;
					}
			
			return value;
		}
			catch(Throwable t)
			{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
		
		
	}
	
	/**
	 * @description: VerifyRadioButtonIsNotSet
	 * @param 	data - value to verify
	 * @return Pass or Fail
	 * @author Parvez
	 * @Date	Mar-11-2014
	 */
	public static String VerifyRadioButtonIsNotSet(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			switchToFrame();
			String value = null;
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.id(Objects.getProperty(object))));
			WebElement check = driver.findElement(By.id(Objects.getProperty(object)));
			
			System.out.println(check.getAttribute("value"));
			if (!check.isSelected())
					{
						value=PASS;
					}
			
			return value;
		}
			catch(Throwable t)
			{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
		
		
	}
		public static String Refresh(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			selenium.refresh();
			//Thread.sleep(10000);
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

		public static String RefreshBrowser(){
			try{
				logger.log(Level.INFO,"Executing keyword: " + keyword);
				driver.navigate().refresh();
				////Thread.sleep(5000);
				return PASS;
			}catch(Throwable t){
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}

	public static String verifyEqualText()
	{
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(Objects.getProperty(object));
			System.out.println("data= " + data);
			String text=driver.findElement(By.xpath(Objects.getProperty(object))).getText();
			System.out.println("text= " + text);
			AutomationException.assertEquals("Two strings are not equal", data, text);
			return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	public static String verifyObjectNotPresent()
	{
		try
		{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			System.out.println(Objects.getProperty(object));
			System.out.println("data= " + data);
			if (driver.findElement(By.xpath(Objects.getProperty(object))).isDisplayed())
			{
				return FAIL;	
			}
			
			else
			{
				return PASS;
			}
			
		}
		
		catch(Throwable t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	public static String clickat(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			selenium.clickAt(Objects.getProperty(object), data);
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	public static String doubleclickat(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			selenium.doubleClickAt(Objects.getProperty(object), data);
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	public static String ClickonFileUpload(){
		try{
			////Thread.sleep(3000);
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			WebElement link = driver.findElement(By.xpath(Objects.getProperty(object)));
			link.click();
			link.click();
			/*selenium.doubleClickAt(Objects.getProperty(object), data);*/
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	// Clicking on a object by fireevent keyword
	public static String fireevent(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			selenium.fireEvent(Objects.getProperty(object),"click");
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	// Clicking on a object by checkBox keyword
	public static String checkBox(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			switchToFrame();
//			wait = new WebDriverWait(driver, 120);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
	        wait.until(ExpectedConditions.visibilityOfElementLocated(By.name(Objects.getProperty(object))));
			WebElement check = driver.findElement(By.name(Objects.getProperty(object)));
			check.click();
			////Thread.sleep(10000);
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	

	public static String scrollPage(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String scrollValueColumn = listTsData.get(0);
			String stringColumn = listTsData.get(1);
					
			String scrollValue = testData.getCellData(currentFTID, scrollValueColumn, currentTCID);
			scrollValue = scrollValue.substring(0, scrollValue.indexOf("."));
			String expectedString = testData.getCellData(currentFTID, stringColumn, currentTCID);
					
			int maxScrollValue = Integer.parseInt(scrollValue.trim());
			System.out.println("maxScrollValue = " + maxScrollValue);
			
		/*	SikuliLib.sikuliScrollPage(maxScrollValue, expectedString);*/
			return PASS;
		}
		catch(Exception t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	/**
	 * Scroll the web page until match expected text and stop
	 * @usage param1 - The expected text
	 * @return Pass or Fail
	 */
	public static String scrollPages(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String expectedString = testData.getCellData(currentFTID, tsData, currentTCID);
			String startPointImage = CONFIG.getProperty("sikuli_scroll_start_point");
			/*int maxScrollValue = Integer.parseInt(CONFIG.getProperty("sikuli_scroll_count"));*/
			
			/*boolean isPageScrolled = SikuliLib.isPageScrolled(startPointImage, maxScrollValue, expectedString);*/
			/*AutomationException.assertTrue("Could not scroll the page", isPageScrolled);*/
			return PASS;
		}
		catch(Exception t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

	public static String clickWinButton(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String expectedString = testData.getCellData(currentFTID, tsData, currentTCID);
			//String startPointImage = CONFIG.getProperty("sikuli_scroll_start_point");
			//int maxScrollValue = Integer.parseInt(CONFIG.getProperty("sikuli_scroll_count"));
			
			/*boolean imgObj = SikuliLib.clickImage(expectedString);*/
			/*AutomationException.assertTrue("Could not find the image", imgObj);*/
			return PASS;
		}
		catch(Exception t)
		{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	
	
	

	/**
     * Description: verify that object is displayed on CFA webpage
     * @param: none
     * @author Huy Nguyen (ndhuy1@tma.com.vn)
	 * @Date: 17/12/2013
	 */
	public static String verifyObjectDisplay() throws IOException{
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
//			wait = new WebDriverWait(driver, 120);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
			boolean check = SeleniumLib.isElementPresent(driver, Objects.getProperty(object));
			AutomationException.assertTrue("Object not display", check);
			return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
					
	}
	public static String verifyObjectDisplaybyText(){
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
//			wait = new WebDriverWait(driver, 20);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			wait.until(ExpectedConditions.presenceOfElementLocated(By.linkText(Objects.getProperty(object))));
			boolean check = SeleniumLib.isElementPresent(driver, Objects.getProperty(object));
			AutomationException.assertTrue("Object not display", check);
			return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
		/**
     * Description: switch to new browser
     * @param: none
     * @author Huy Nguyen (ndhuy1@tma.com.vn)
	 * @Date: Mar-14-2014
	 */
	public static String switchToNewBrowser(){
		try{
			winHandleBefore = driver.getWindowHandle();
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			//Thread.sleep(20000);	
			WebDriver popup = null;
		    Iterator<String> windowIterator = driver.getWindowHandles().iterator();
		    while(windowIterator.hasNext())
		    { 
		    	String windowHandle = windowIterator.next(); 
		    	popup = driver.switchTo().window(windowHandle);
		    	if(popup.getTitle().contains(CONFIG.getProperty("Title")))
				{
					driver.get("javascript:document.getElementById('overridelink').click();");
					System.out.println(popup.getTitle());
		    		break;
				}
		    }
			return PASS;
		}catch(Throwable t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	/**
	 * @description: verify text contains substring
	 * @category
	 * @usage: 	
	 * 			data: data contain
	 * @return Pass or Fail
	 * @author Huy Nguyen (ndhuy1@tma.com.vn)
	 * @Date	Mar-14-2014
- */
	public static String verifyTextContain()
	{
		try{
			logger.log(Level.INFO,"Executing keyword: " + keyword);
			String data = testData.getCellData(currentFTID, tsData, currentTCID);
			// If value is a key, the real value will be getting from Property file
			if(CommonData.containsKey(data)){
				data = CommonData.getProperty(data);
			}
			String text=driver.findElement(By.xpath(Objects.getProperty(object))).getText();
			System.out.println("text= " + text);
			AutomationException.assertContains("String not contains substring", data, text);
			logger.log(Level.INFO,"String contains substring");
			return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}
	
	/**
 * @description: get current text in dropdowm
 * @param 	data - data to compare
 * @return Pass or Fail
 * @author Huy Nguyen (ndhuy1@tma.com.vn)
 * @Date	Mar-20-2014
 */
public static String getTextFromDropdown()
{
	try{
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		String data = testData.getCellData(currentFTID, tsData, currentTCID);
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		String text = element.getAttribute("value");
		System.out.println("text= " + text);
		AutomationException.assertEquals("Two strings are not equal", data, text);
		return PASS;
	}catch(Exception t){
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
}
/**
 * @description: navigate to back in web browser
 * @return Pass or Fail
 * @author Huy Nguyen (ndhuy1@tma.com.vn)
 * @Date	Mar-20-2014
 */

public static String getQuoteNumber()
{
	try{
		////Thread.sleep(5000);
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		String text = element.getText();
		System.out.println("text= " + text);
		List<String> lines = Arrays.asList(text);
		Path file = Paths.get("D:\\Automation\\Getquotenumber.txt");
		Files.write(file, lines, Charset.forName("UTF-8"));
		Files.write(file, lines, Charset.forName("UTF-8"), StandardOpenOption.APPEND);
		return PASS;
	}catch(Exception t){
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
}

public static String navigateBack()
{
	try{
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		driver.navigate().back();
		////Thread.sleep(5000);
		return PASS;
	}catch(Exception t){
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
}


public static String Datepicker()
{
	try{
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		// Value is getting from excel file
	//	String data = testData.getCellData(currentFTID, tsData, currentTCID);
		//System.out.println(Objects.getProperty(object));
		//System.out.println(data);
		
		//////Thread.sleep(1000);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			WebElement month = driver.findElement(By.xpath(Objects.getProperty(object)));
			
			WebElement year=driver.findElement(By.xpath(Objects.getProperty(object)));
			
		  org.openqa.selenium.support.ui.Select monthclick=new org.openqa.selenium.support.ui.Select(month);
		  
		  //Sleeper.sleepTightInSeconds(5);
		  
		  monthclick.selectByVisibleText("April");
		  //Sleeper.sleepTightInSeconds(3);
		  
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));

            org.openqa.selenium.support.ui.Select yearclick=new org.openqa.selenium.support.ui.Select(year);
            //Sleeper.sleepTightInSeconds(4);
		  
		    yearclick.selectByVisibleText("2016");
			
		    //Sleeper.sleepTightInSeconds(4);
			
		
        return PASS;
	}catch(Exception t){	
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
}


public static String SelectMonth()
{
	try{

        ////Thread.sleep(1000);
        logger.log(Level.INFO,"Executing keyword: " + keyword);
        
        text=testData.getCellData(currentFTID, tsData, currentTCID);
        
//			wait = new WebDriverWait(driver, 90);
        driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			WebElement month = driver.findElement(By.xpath(Objects.getProperty(object)));
			
			
		org.openqa.selenium.support.ui.Select monthclick=new org.openqa.selenium.support.ui.Select(month);
		 
			
		 //Sleeper.sleepTightInSeconds(5);
		 monthclick.selectByVisibleText(text);
		 //Sleeper.sleepTightInSeconds(3);
		  
			
        return PASS;
	}catch(Exception t){	
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
}









public static String SelectCity()
{
	try{
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		// Value is getting from excel file
	//	String data = testData.getCellData(currentFTID, tsData, currentTCID);
		//System.out.println(Objects.getProperty(object));
		//System.out.println(data);
		
		//////Thread.sleep(1000);
			driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
			
			
			
			
			wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));

            WebElement city = driver.findElement(By.xpath(Objects.getProperty(object)));
			
			//Sleeper.sleepTightInSeconds(5);
			

           org.openqa.selenium.support.ui.Select city1=new org.openqa.selenium.support.ui.Select(city)	;
            city1.selectByVisibleText("Chennai");
		  
		  
			
		
        return PASS;
	}catch(Exception t){	
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
}




public static String randomnum(){
    try{
           logger.log(Level.INFO,"Executing keyword: " + keyword);
           // Value is getting from excel file

           Random rndNum= new Random(); 

              String number = null;
			for (int nbr = 1; nbr <= 1; nbr++) {
                  int rndNum1 = rndNum.nextInt();
                  rndNum1=rndNum1<0 ? rndNum1 *-1 : rndNum1;
                  number=String.valueOf(rndNum1);
                  System.out.println("Number: " + rndNum1);    }
    //     ////Thread.sleep(1000);
                  driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
                  wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
                  WebElement entertext = driver.findElement(By.xpath(Objects.getProperty(object)));
                  entertext.clear();   
                  entertext.sendKeys(number);
    
           
     return PASS;
    }catch(Exception t){ 
           logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
           return FAIL;
    }
}

public static String SelectDropDownElement(){
    try{
           logger.log(Level.INFO,"Executing keyword: " + keyword);
           
         WebElement drop= driver.findElement(By.xpath("//select[@name='searchedRunNumber']"));
       //  drop.click();
         Sleeper.sleepTightInSeconds(2);
         
         org.openqa.selenium.support.ui.Select run=new org.openqa.selenium.support.ui.Select(drop);
         
         Sleeper.sleepTightInSeconds(1);
         
         run.selectByIndex(1);
        
         
         
         
              
           
     return PASS;
    }catch(Exception t){ 
           logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
           return FAIL;
    }
}




public static String Selectcoveragepagecheckbox(){
    try{
           logger.log(Level.INFO,"Executing keyword: " + keyword);
           
        
           

         List<WebElement> els = driver.findElements(By.xpath("//input[@type='checkbox']"));
         wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//input[@type='checkbox']")));

         
         
         for ( WebElement el : els ) {
         if ( !el.isSelected() ) 
         {
        el.click();
          }
        }
         
         
         
              
           
     return PASS;
    }catch(Exception t){ 
           logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
           return FAIL;
    }
}




public static String selectallcheckbox(){
       try{
              logger.log(Level.INFO,"Executing keyword: " + keyword);
              List<WebElement> els = driver.findElements(By.xpath("//input[@type='checkbox']"));
              wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//input[@type='checkbox']")));
                           for ( WebElement el : els ) {
                  if ( !el.isSelected() ) {
                      el.click();
                  }
              }
              
              return PASS;
       }
              catch(Throwable t)
              {
              logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
              return FAIL;
       }
       
}

       



public static String calculatepremium()
{
       try{
              ////Thread.sleep(1000);
              logger.log(Level.INFO,"Executing keyword: " + keyword);
              
              text=testData.getCellData(currentFTID, tsData, currentTCID);
              
            // text=text.replaceAll(",", "");
              //text=text.substring(0,text.indexOf("."));
              
              
              int x=(int)Math.ceil(Double.parseDouble(text));
              System.out.println("NET PREMIUM VALUE:"+x);
              
              float param2=(float)(((x)*(0.5/100)));
              int swach=Math.round(param2);
              System.out.println("SWACH BHARAT TAX:"+swach);
              
              float param1=(float)(( (x) * (0.14) )); 
              int stax=Math.round(param1);
              System.out.println("SERVICE TAX :"+stax);
                     
              float param3=(float)(((x)*(0.5/100)));
              int etax=Math.round(param3);
              System.out.println("EDUCATIONAL TAX :"+etax);
               
                sum=swach+stax+etax+x;
                System.out.println("SUM OF ALL :"+sum);
                
                int z=Math.round(sum);
                System.out.println("AFTER ADDING ALL TAXES VALUE :"+z);
                
                     driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
                     wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//table[2]/tbody/tr")));
                     List<WebElement> row1 = driver.findElements(By.xpath("//table[2]/tbody/tr"));
                     System.out.println("TOTAL ROW SIZE :"  +row1.size());
                     for(int i=row1.size();i<=row1.size();i++)
                     {
                           
                           WebElement net=driver.findElement(By.xpath("//table[2]/tbody/tr["+ i +"]/td[4]"));
                           String payable=net.getText();
       
                                  //System.out.println(payable);
                                  payable1 = Integer.parseInt(payable);
                     }
             System.out.println("TOTAL PREMIUM IS :"+payable1);
              //Assert.assertEquals(z, payable1);
              //Sleeper.sleepTightInSeconds(6);
             
             if (z!= payable1)
             {
            	 logger.log(Level.WARNING,"Basic Net Premium  and Actual Payable not equal");
            	 return FAIL; 
             }
             else
             {
            	 return PASS;
             }
              
             
              }catch(Exception t){
                     logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
                     return FAIL;
              }
       }


public static String netpremium()
{
       try{
              //Thread.sleep(2000);
              logger.log(Level.INFO,"Executing keyword: " + keyword);
              ////Thread.sleep(1000);
              driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
              wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//table[2]/tbody/tr")));
              List<WebElement> row1 = driver.findElements(By.xpath("//table[2]/tbody/tr"));
              System.out.println("size of net premium"  +row1.size());
              for(int i=row1.size()-4;i<=row1.size()-4;i++)
              {
                    
                    WebElement net=driver.findElement(By.xpath("//table[2]/tbody/tr["+ i +"]/td[4]"));
                    text = net.getText();
                   
              }
              return PASS;
              }catch(Exception t){
                    logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
                    return FAIL;
              }
}




public static String calculatepremiumCapture()
{
       try{
              ////Thread.sleep(1000);
              logger.log(Level.INFO,"Executing keyword: " + keyword);
              
               text=text.replaceAll(",", "");
            // text=text.substring(0,text.indexOf("."));
              
              
              
              int x=(int)Math.ceil(Double.parseDouble(text));
              System.out.println("NET PREMIUM VALUE:"+x);
              
              float param2=(float)(((x)*(0.5/100)));
              int swach=Math.round(param2);
              System.out.println("SWACH BHARAT TAX:"+swach);
              
              float param1=(float)(( (x) * (0.14) )); 
              int stax=Math.round(param1);
              System.out.println("SERVICE TAX :"+stax);
                     
              float param3=(float)(((x)*(0.5/100)));
              int etax=Math.round(param3);
              System.out.println("EDUCATIONAL TAX :"+etax);
               
                sum=swach+stax+etax+x;
                System.out.println("SUM OF ALL :"+sum);
                
                int z=Math.round(sum);
                System.out.println("AFTER ADDING ALL TAXES VALUE :"+z);
                
                     driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
                     wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//table[2]/tbody/tr")));
                     List<WebElement> row1 = driver.findElements(By.xpath("//table[2]/tbody/tr"));
                     System.out.println("TOTAL ROW SIZE :"  +row1.size());
                     for(int i=row1.size();i<=row1.size();i++)
                     {
                           
                           WebElement net=driver.findElement(By.xpath("//table[2]/tbody/tr["+ i +"]/td[4]"));
                           String payable=net.getText();
       
                                  System.out.println(payable);
                                  payable1 = Integer.parseInt(payable);
                     }
              System.out.println("TOTAL PREMIUM IS :"+payable1);
              Assert.assertEquals(z, payable1);
              //Sleeper.sleepTightInSeconds(6);
              
              return PASS;
              }catch(Exception t){
                     logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
                     return FAIL;
              }
       }

		/**
		 * Assert a given text to see if it is present in the web page 
		 * 
		 * @usage parameter1 - The expected string
		 * @return 	PASS - If expected string is appeared on the page, 
		 * 			FAIL - If expected is not appeared or an exception occurred
		 */
		public static String assertMsgPresentOnPage(){
			try{
				logger.log(Level.INFO,"Executing keyword: " + keyword);
				String expectedMsg = testData.getCellData(currentFTID, tsData, currentTCID);
				AutomationException.assertTrue("Expected text is not appreared", SeleniumLib.isMsgPresentOnPage(driver, expectedMsg));
				return PASS;
			}
			catch(Throwable t)
			{
				logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
				return FAIL;
			}
		}
		
		
		public static String assertIntegerValue() {
		       try{
		            
		              logger.log(Level.INFO,"Executing keyword: " + keyword);
		              
		              text=testData.getCellData(currentFTID, tsData, currentTCID);
		              logger.log(Level.INFO,"Basic Premium : " + text);
		           
		              int x=(int)Math.ceil(Double.parseDouble(text));
		              System.out.println("Basic TP Value:"+x);
		             
		                     driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
		                     
		                     wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));                     
		                     WebElement Actual_Value=driver.findElement(By.xpath(Objects.getProperty(object)));
		                     
		                     String tp_actual_value=Actual_Value.getText();             
		                     logger.log(Level.INFO,"Actual Premium : " + tp_actual_value);
		                     int y = (int)Math.ceil(Double.parseDouble(tp_actual_value));
		              System.out.println("Actual Value is:"+tp_actual_value);
		             if (x != y)
		             {
		            	 logger.log(Level.WARNING,"Basic Value and Actual Value is not equal");
		            	 return FAIL; 
		             }
		             else
		             {
		            	 return PASS;
		             }
		            
		             
		              }catch(Exception t){
		                     logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		                     return FAIL;
		              }
		       }
		


public static String SelectByIndex(){
    try{
           logger.log(Level.INFO,"Executing keyword: " + keyword);
           String data = testData.getCellData(currentFTID, tsData, currentTCID);
           
           
           WebElement drop= driver.findElement(By.xpath(Objects.getProperty(object)));
           org.openqa.selenium.support.ui.Select Sel=new org.openqa.selenium.support.ui.Select(drop);
           Sel.selectByIndex((int)Math.ceil(Double.parseDouble(data)));    
 
     return PASS;
    }catch(Exception t){ 
           logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
           return FAIL;
    }
}


/**
 * Input IDV value for text box
 * @param param1 - The value that need to fill into text box
 * @return Pass or Fail
 */
public static String inputIDVValue(){
	try{
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		// Value is getting from excel file
		String data = testData.getCellData(currentFTID, tsData, currentTCID);
		//System.out.println(Objects.getProperty(object));
		System.out.println(data);
		
	//	////Thread.sleep(1000);
//		wait = new WebDriverWait(driver, 90);
		driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
		wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
		String ListPrice = driver.findElement(By.xpath(Objects.getProperty("ListPrice"))).getAttribute("value");
		
		WebElement entertext = driver.findElement(By.xpath(Objects.getProperty(object)));
		entertext.clear();
        entertext.sendKeys(ListPrice);
     	entertext.sendKeys(Keys.TAB);
	
		
        return PASS;
	}catch(Exception t){	
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}
}

public static String clickCashLink(){
    try{
           logger.log(Level.INFO,"Executing keyword: " + keyword);
           ////Thread.sleep(3000);
           String text = driver.findElement(By.xpath("//td[text()='Total Premium :']/following::td[1]")).getText();  
           logger.log(Level.INFO,"Premium Value : "+ text);
                      
           String Val1 = text.substring(0, text.indexOf(','));
           String Val2 = text.substring(text.indexOf(',')+1, text.length()-1);
           String Value = Val1+Val2;
           
          int Premium = (int)Math.ceil(Double.parseDouble(Value));
          logger.log(Level.INFO,"converted to int : "+ Value);
           if(Premium >=100000)
           {
        	   logger.log(Level.INFO,"Filling Pan Card Number");
        	   driver.findElement(By.xpath("//input[@id='panNumber']")).sendKeys("PFFRS3411H");
        	   driver.findElement(By.xpath("//img[@id='paysubmitimage']")).click();
        	   SwitchToAlert();
           }
           wait.until(ExpectedConditions.visibilityOfElementLocated(By.linkText(Objects.getProperty(object))));
           WebElement link = driver.findElement(By.linkText(Objects.getProperty(object)));
//           wait = new WebDriverWait(driver, 90);
           driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
     //wait.until(ExpectedConditions.visibilityOfElementLocated(By.linkText(Objects.getProperty(object))));
           wait.until(ExpectedConditions.presenceOfElementLocated(By.linkText(Objects.getProperty(object))));
           link.click();
           
           /*String certificate = CONFIG.getProperty("CertificateErr");*/
           /*Screen scr = new Screen();
           if (scr.exists(certificate) != null){
                 SikuliLib.clickImage(certificate);
                 ////Thread.sleep(5000);
                 scr.type(Key.DOWN);
                 scr.type(Key.ENTER);
                 scr.mouseMove(scr.getCenter());
                 //Thread.sleep(20000);
           }*/
           return PASS;
    }catch(Throwable t){
           logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
           return FAIL;
    }
}

public static String getQuoteNo()
{
	try{
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		////Thread.sleep(1000);
		driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
		wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
		
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		text = element.getText().trim();
		System.out.println("Quote Number : " + text);
		logger.log(Level.INFO,"Quote Number : " + text);
		return PASS;
		}
	catch(Exception t)
	{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;		
	}	
}

public static String getPolicyNo()
{
	try{
		//Thread.sleep(2000);
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		////Thread.sleep(1000);
		driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
		wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
		
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		text = element.getText().trim();
		System.out.println("Policy Number :  " + text);
		logger.log(Level.INFO,"Policy Number : " + text);
		return PASS;
		}
	catch(Exception t)
	{
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;		
	}
}


public static String Select_Setting_Capacity(){
    try{
           logger.log(Level.INFO,"Executing keyword: " + keyword);
      
           
         WebElement drop= driver.findElement(By.xpath("//select[@name='seatingCapacity']"));
         //Sleeper.sleepTightInSeconds(5);
           
         org.openqa.selenium.support.ui.Select SeatingCapacity=new org.openqa.selenium.support.ui.Select(drop);
         //Sleeper.sleepTightInSeconds(3);
         waitSometime();
         SeatingCapacity.selectByIndex(1);     
         
         
         
              
           
     return PASS;
    }catch(Exception t){ 
           logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
           return FAIL;
    }
}

public static String calculate_TP_premium()
{
   try{
          ////Thread.sleep(1000);
          logger.log(Level.INFO,"Executing keyword: " + keyword);
          
          text=testData.getCellData(currentFTID, tsData, currentTCID);
          logger.log(Level.INFO,"Basic Premium : " + text);
       
          int x=(int)Math.ceil(Double.parseDouble(text));
          System.out.println("Basic TP Value:"+x);
         
                 driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
                 
                 wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//table[2]/tbody/tr[4]/td[6]")));                     
                 WebElement Actual_Value=driver.findElement(By.xpath("//table[2]/tbody/tr[4]/td[6]"));
                 
                 String tp_actual_value=Actual_Value.getText();             
                 logger.log(Level.INFO,"Actual Premium : " + tp_actual_value);
                 int y = (int)Math.ceil(Double.parseDouble(tp_actual_value));
          System.out.println("Actual Value is:"+tp_actual_value);
         if (x != y)
         {
        	 logger.log(Level.WARNING,"Basic Value and Actual Value is not equal");
        	 return FAIL; 
         }
         else
         {
        	 return PASS;
         }
         /* Assert.assertEquals(x, tp_actual_value);
          //Sleeper.sleepTightInSeconds(6);
          
          return PASS;*/
         
         
          }catch(Exception t){
                 logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
                 return FAIL;
          }
   }

public static String calculate_TP_premium_PPC_MC()
{
   try{
          ////Thread.sleep(1000);
          logger.log(Level.INFO,"Executing keyword: " + keyword);
          
          text=testData.getCellData(currentFTID, tsData, currentTCID);
          logger.log(Level.INFO,"Basic Premium : " + text);
       
          int x=(int)Math.ceil(Double.parseDouble(text));
          System.out.println("Basic TP Value:"+x);
         
                 driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
                 
                 wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath("//table[2]/tbody/tr[3]/td[4]")));                     
                 WebElement Actual_Value=driver.findElement(By.xpath("//table[2]/tbody/tr[3]/td[4]"));
                 
                 String tp_actual_value=Actual_Value.getText();             
                 logger.log(Level.INFO,"Actual Premium : " + tp_actual_value);
                 int y = (int)Math.ceil(Double.parseDouble(tp_actual_value));
          System.out.println("Actual Value is:"+tp_actual_value);
         if (x != y)
         {
        	 logger.log(Level.WARNING,"Basic Value and Actual Value is not equal");
        	 return FAIL; 
         }
         else
         {
        	 return PASS;
         }
         /* Assert.assertEquals(x, tp_actual_value);
          //Sleeper.sleepTightInSeconds(6);
          
          return PASS;*/
         
         
          }catch(Exception t){
                 logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
                 return FAIL;
          }
   }






public static String getBatchID()
{
	try{
		//Thread.sleep(2000);
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		////Thread.sleep(1000);
		driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
		wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
		
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		text = element.getText();
		System.out.println("text= " + text);
		
		return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}



public static String putBatchID()
{
	try{
		//Thread.sleep(2000);
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		text=text.replaceAll(",", "");
		
		//text=text.substring(0,text.indexOf("."));
		element.sendKeys(text);
		System.out.println("text= " + text);
		return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}


public static String GetRenewedPolicyNumber() {
    try {                
           logger.log(Level.INFO, "Original Policy Number : " + text);

           String text1 = text.replaceAll("\\D+", "");
           String str = text1.substring(text1.length()-3);
           int x = (int) Math.ceil(Double.parseDouble(str));             
           x= x+1;
           String str1 = String.valueOf(x);  
           str = text.replace(text.substring(text.length()-3), str1);           
           WebElement element = driver.findElement(By.xpath(Objects.getProperty(object)));
           element.sendKeys(str);
           logger.log(Level.INFO, "Policy Number : " + str);
           System.out.println("Policy Number : " + str);
           return PASS;
    } catch (Throwable t) {
           logger.log(Level.WARNING, "Failed with reason: " + t.getMessage());
           return FAIL;
    }
}

  

  


public static String getECoverNote()
{
	try{    
		//Thread.sleep(2000);
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		////Thread.sleep(1000);
		driver.manage().timeouts().implicitlyWait(60, TimeUnit.SECONDS);
		wait.until(ExpectedConditions.visibilityOfElementLocated(By.xpath(Objects.getProperty(object))));
		
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		Ecovernote = element.getText();
		System.out.println("Ecovernote= " + Ecovernote);
		
		return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}



public static String putECovernote()
{
	try{
		//Thread.sleep(2000);
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		WebElement element=driver.findElement(By.xpath(Objects.getProperty(object)));
		Ecovernote=Ecovernote.replaceAll(",", "");
		
		//text=text.substring(0,text.indexOf("."));
		element.sendKeys(Ecovernote);
		System.out.println("Ecovernote= " + Ecovernote);
		return PASS;
		}catch(Exception t){
			logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
			return FAIL;
		}
	}

public static String PDFReader()
{
	try{
		
		logger.log(Level.INFO,"Executing keyword: " + keyword);
		
		  
		  Thread.sleep(5000);
		  URL url=new URL(driver.getCurrentUrl());
		  //BufferedInputStream fileToParse = new BufferedInputStream(
		  //url.openStream());
		  //parser = new PDFParser(fileToParse);
		  //parser.parse();
		  
		  PDDocument document = PDDocument.load(url);

		  //String output = new PDFTextStripper().getText(parser.getPDDocument());
		  
		  String output = new PDFTextStripper().getText(document);

		  if (output.contains("Royal Sundaram General Insurance Co. Limited")) 
		  {
			System.out.println("Royal Sundaram General Insurance Co. Limited Exit in PDF");
		  }
		  else
		  {
			  System.out.println("Royal Sundaram General Insurance Co. Limited not Exit in PDF");
		  }
		
		  System.out.println(output);
		  logger.log(Level.WARNING,"Text present pdf file : " + output);
		return PASS;
	}catch(Throwable t){
		
		
		logger.log(Level.WARNING,"Failed with reason: " + t.getMessage());
		return FAIL;
	}

}

}//end class
