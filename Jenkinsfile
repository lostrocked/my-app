    def boolean login(String url, String userid, String pw)
    {
     this.url = url;
     this.userid = userid;
     this.pw = pw;
     
     def res = doGetHttpRequestWithJson("${url}/dmadminweb/API/login?user=" + enc(userid) + "&pass=" + enc(pw));
     
     return res.success;
    }
    
    def moveApplication(String url, String userid, String pw, String Application, String FromDomain, String Task)
    {
     if (this.url.length() == 0)
     {
      if (!login(url,userid,pw))
       return [false,"Could not login to " + url];
     }
     // Get appid
     def data = doGetHttpRequestWithJson("${url}/dmadminweb/API/application/" + enc(Application));
     def appid = data.result.id;
     
     // Get from domainid
     data = doGetHttpRequestWithJson("${url}/dmadminweb/API/domain/" + enc(FromDomain));
     def fromid = data.result.id;
     
     // Get from Tasks
     data = doGetHttpRequestWithJson("${url}/dmadminweb/GetTasks?domainid=" + fromid);
     if (data.size() == 0)
      return [false,"Could not move the Application '" + Application + "' from '" + FromDomain + "' using the '" + Task + "' Task"];

      def i=0;
      def taskid = 0;
      for (i=0;i<data.size();i++)
      {
       if (data[i].name.equalsIgnoreCase(Task))
       {
        taskid = data[i].id;
        break;
       }
