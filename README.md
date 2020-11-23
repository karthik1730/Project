var token ="1245391439:AAERI9-Tst0HguFYfPHDEGe6mvh-Xdrkm2E";
var telegramUrl = "https://api.telegram.org/bot"+token;
var webAppUrl = "https://script.google.com/macros/s/AKfycbx_MclWC8Ak08OCayAaUY0_FqDq3rib_jx6sUsVAyc28lWJxH5b/exec";
var ssId="1-9M2PQRNH9RMwWZP5q1QHDWW3_p0pY28eaHZHlm4FUM";
function getMe() {
  var url = telegramUrl+"/getMe";
  var response =UrlFetchApp.fetch(url);
  Logger.log(response.getContentText());
}
function setWebhook(){
  var url = telegramUrl+"/setWebhook?url=" + webAppUrl;
  var response =UrlFetchApp.fetch(url);
  Logger.log(response.getContentText()); 
}
function sendText(id,text){
  var url = telegramUrl+"/sendMessage?chat_id=" +id + "&text=" + text;
  var response =UrlFetchApp.fetch(url);
  Logger.log(response.getContentText());
  
}
function doGet(e){
  return HtmlService.createHtmlOutput("Hii fam"); 
}
function doPost(e){
  //this is where we post our messages in telegram
  var data = JSON.parse(e.postData.contents);
  var text = data.message.text;
  var id = data.message.chat.id;
  var name = data.message.chat.first_name + " " + data.message.chat.last_name;
  var answer = "Hi How are you?";
  if(text == "hi"||text == "Hi"||text=="Hello"||text =="hello"||text=="Hiiiii"){
  sendText(id,answer);
  }
    if(text == "crazy"||text == "pikinav thi"||text=="vacchesadu"||text =="edava"||text=="aapara"){
      var answers= "Maamuluga undadu";
  sendText(id,answers);
  }
  SpreadsheetApp.openById(ssId).getSheets()[0].appendRow([new Date(),id,name,text,answer]);
  
  if(/^@/.test(text)){
     var sheetName = text.slice(1).split(" ")[0];
    var sheet =SpreadsheetApp.openById(ssId).getSheetByName(sheetName)? SpreadsheetApp.openById(ssId).insertSheet(sheetName) : SpreadsheetApp.openById(ssId).insertSheet(sheetName)
     var comment = text.split(" ").slice(1).join(" ");
  sheet.appendRow([new Date(),id,name,comment,answer]);
}
}
/*
{
    "update_id": 82029458,
    "message": {
        "message_id": 9,
        "from": {
            "id": 951668226,
            "is_bot": false,
            "first_name": "Karthik",
            "last_name": "1730",
            "username": "Karthik1730",
            "language_code": "en"
        },
        "chat": {
            "id": 951668226,
            "first_name": "Karthik",
            "last_name": "1730",
            "username": "Karthik1730",
            "type": "private"
        },
        "date": 1594724058,
        "text": "Hii"
    }
}
{
    "parameters": {},
    "parameter": {},
    "contentLength": 316,
    "contextPath": "",
    "queryString": "",
    "postData": {
        "contents": "{\"update_id\":82029453,\n\"message\":{\"message_id\":4,\"from\":{\"id\":951668226,\"is_bot\":false,\"first_name\":\"Karthik\",\"last_name\":\"1730\",\"username\":\"Karthik1730\",\"language_code\":\"en\"},\"chat\":{\"id\":951668226,\"first_name\":\"Karthik\",\"last_name\":\"1730\",\"username\":\"Karthik1730\",\"type\":\"private\"},\"date\":1594722501,\"text\":\"Hii\"}}",
        "length": 316,
        "name": "postData",
        "type": "application/json"
    }
}
*/
