# sms_api_ug
Sends SMS via ego sms api

HTTP PLAIN GET API UsageThe API provides a solution to send message via HTTP using your account details.Required Details URL:Parameters:These are separated using the and signjust like in a normal http get.

Number: This represents the URL encoded phone number.

Message:This represents the URL encoded SMS youare sending out. The message source Must havea maximum of 160 characters.

Sender:This represents who the message is coming from. Sender can have a maximum of 11 Characters and needs to be URL encoded too.

Username:The API callers username used to login to Egosms.

Password:The API callers password used to login to Egosms.

System Feedback Once your message has been successfully sent to the network the system will show Sent, otherwise it will show Error. URL Example:
You can send SMS by just calling a link. e.g.The above link will send the message “My First Message through Egosms” to256774733492using thelogin detailsEgosmstestand password egotest:

http://www.egosms.co/api/v1/plain/?number=%2B256774733492&message=My+First+Message+Through+Egosms&username=Egosmstest&password=egotest&sender=Egosms

http://www.egosms.co/api/v1/plain/

Alternatively you can send the message directly from your software below is a PHP Example

<?phpfunction SendSMS($username,$password,$sender,$number,$message)
{$parameters="number=[number]&message=[message]&username=[username]&password=[password]&sender=[sender]";$parameters = str_replace("[message]", urlencode($message), $parameters);$parameters = str_replace("[sender]", urlencode($sender),$parameters);$parameters = str_replace("[number]", urlencode($number),$parameters);$parameter
s = str_replace("[username]", urlencode($username),$parameters);$parameters = str_replace("[password]", urlencode($password),$parameters);$live_url="http://".$url.$parameters;$parse_url=file($live_url);$response = $parse_url[0];return $response;}$username ="Egosmstest";$password ="egotest";$sender ="Egosms";$number ="+256774733492";$message ="My First Message through Egosms";echo SendSMS($username,$password,$sender,$number,$message);?>The above PHP code will send the message“My First Message through Egosms” to256774733492Using the login detailsEgosmstest and passwordegotest$url = "www.egosms.co/api/v1/plain/?";

Explanation of parameters Parameter Type Required Meaning UsernamestringmandatoryAccount userPasswordStringmandatoryEncoded passwordSenderStringmandatorySender id of the messageNumberStringmandatoryPhone numberMessagestringmandatoryMessage to be sent 

HTTP XML APIUsageSending sms using xml API Request<?xml version="1.0" encoding="UTF-8"?><Request><userdata>---</userdata><msgdata>----</msgdata></Request>Response<?xml version="1.0" encoding="UTF-8"?><Response><Status>xxxxx</Status>-----</Response>System FeedbackOnce your message has been successfully submitted to the EgoSms system, it will return xml in the format shown below:SuccessFormat<?xml version="1.0" encoding="UTF-8"?><Response><Status>OK</Status><Cost>---</Cost><MsgFollowUpUniqueCode>---</MsgFollowUpUniqueCode></Response>Otherwise the system will returnxml in the format shown below:FailedFormat<?xml version="1.0" encoding="UTF-8"?><Response><Status>Failed</Status><Message>---</Message></Response>XML path: http://www.egosms.co/api/v1/xml/
©2012-2014 EgoSms , Inc. All Rights Reserved.Page 8EXAMPLE Submited XML<? Xml version="1.0" encoding="UTF-8"?><Request><method>SendSms</method><userdata><username>Dokole</username><password>K01234</password></user data><msgdata><number>256705691069</number><message>welcome to Egosms</message><senderid>Egosms</senderid></msgdata></Request>System FeedbackReturned XML For a Successful RequestOnce your message has been successfully submitted to the Egosms system, it will return xml in the format shown below:<? Xmlversion="1.0" encoding="UTF-8"?><Response><Status>OK</Status><Cost>35</Cost><MsgFollowUpUniqueCode>ApiXmlSubmit53b5155c1a3f90.65739380</MsgFollowUpUniqueCode></Response>Returned XML For a Failed RequestOtherwise the system will returnxml in the format shown below:<? Xmlversion="1.0" encoding="UTF-8"?><Response><Status>Failed</Status><Message>Error Response message</Message></Response>The Possible Error MessagesWrong Xml PassedMoney Not Enough To Send This Batch of MsgsWrong Username or PasswordThat user does not exist or user not activeEither Username or Password Not Set
©2012-2014 EgoSms , Inc. All Rights Reserved.Page 9PHP Example<?php$xml_builder='<?xml version="1.0" encoding="UTF-8"?><Request><method>SendSms</method><userdata><username>Dokole</username><password>K01234</password></userdata><msgdata><number>256774733492</number><message>testmtn</message><senderid>test</senderid></msgdata><msgdata><number>256705691069</number><message>welcome to Egosms</message><senderid>test</senderid></msgdata></Request>';//use curl to post the xml informationcurl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: text/xml'));curl_setopt($ch, CURLOPT_HEADER, 0);curl_setopt($ch, CURLOPT_POST, 1);curl_setopt($ch, CURLOPT_POSTFIELDS, $xml_builder);curl_setopt($ch, CURLOPT_FOLLOWLOCATION, 0);curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);$ch_result = curl_exec($ch);curl_close($ch);echo $ch_result;?>$ch = curl_init('http://www.egosms.co/api/v1/xml/');
©2012-2014 EgoSms , Inc. All Rights Reserved.Page 10Explanation of parameters Parameter Type Required Meaning User datastringmandatoryUsers informationMsgdatastringmandatoryMessage informationstatusstringmandatoryWhether its ok or Failed deliverycostfloatmandatoryPrice chargedMsgFollowUpUniqueCodestringmandatoryUnique code for message sent
©2012-2014 EgoSms , Inc. All Rights Reserved.Page 11HTTP JSON API UsageSending sms using jsonAPI RequestFormat{"userdata":{"username":"xxxxxx","password":"xxxxxx"},"msgdata":[{"number":"2567xxxxxxxx","message":"xxxxxx","senderid":"xxxxxx"}]}System FeedbackReturned JsonFor a Successful RequestOnce your message has been successfully submitted to the Egosms system, it will return json in the format shown below:Success{"Status":"OK","Cost":"xxxx","MsgFollowUpUniqueCode":"xxxxx"}Returned Json For a Failed RequestOtherwise the system will returnjsonin the format shown below:Failed{"Status":"Failed","Message":"xxxxxx"}EXAMPLE JsonSubmited JSON{"method":"SendSms","userdata":{"username":"Dokole","password":"K01234"},"msgdata":[{"number":"256705691069","message":" welcome to Egosms","senderid":"Egosms"}]}Json path: http://www.egosms.co/api/v1/json/
©2012-2014 EgoSms , Inc. All Rights Reserved.Page 12Returned JSON fora Successful Request{"Status":"OK","Cost":"35","MsgFollowUpUniqueCode":"ApiJsonSubmit53b5155c1a3f90.65989312"}Returned JSON fora Failed Request{"Status":"Failed","Message":"Error Response message"}Error Response:Wrong JSONPassedMoney Not Enough To Send This Batch of MsgsWrong Username or PasswordThat user does not exist or user not activeEither Username or Password Not SetPHP Example<?php$data= array('method'=>'SendSms','userdata'=> array('username'=>'dokole',// Egosms Username'password'=>'K01234' //Egosms Password),'msgdata'=> array(array('number'=>256704733492,'message'=>'elias','senderid'=>'Good'),array('number'=>256774733492,'message'=>'marvin','senderid'=>'Bad')));
©2012-2014 EgoSms , Inc. All Rights Reserved.Page 13
