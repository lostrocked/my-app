// vars/deployhub.groovy
import hudson.model.*
import hudson.EnvVars
import groovy.json.JsonSlurperClassic
import groovy.json.JsonBuilder
import groovy.json.JsonOutput
import java.net.URL
class deployhub {
    String body="";    
    String message="";    
    String cookie="";   
    String url="http://srisa09-l28234.lvn.broadcom.net:8080/datamanagement/a/api/v2/applications";   
    String userid="superuser";
    String pw="suser"; 
    Integer statusCode;    
    boolean failure = false;
    
    def doGetHttpRequest(String requestUrl){    
        URL url = new URL(requestUrl);    
        HttpURLConnection connection = url.openConnection();    
       
        connection.setRequestMethod("GET");
        connection.setRequestProperty("Cookie", cookie); 
        connection.doOutput = true;   
 
        //get the request    
        connection.connect();    
 
        //parse the response    
        parseResponse(connection);    
 
        if(failure){    
            error("\nGET from URL: $requestUrl\n  HTTP Status: $resp.statusCode\n  Message: $resp.message\n  Response Body: $resp.body");    
        }    
 
        this.printDebug("Request (GET):\n  URL: $requestUrl");    
        this.printDebug("Response:\n  HTTP Status: $resp.statusCode\n  Message: $resp.message\n  Response Body: $resp.body");    
    } 
}
