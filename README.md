
## 背景

 * 手贱分析协义

## 概要


### 架构


## 协议

### User Credentials

 **Request:**
 
	http://rc.weitv.me/api/v1/register/device=test&login=1E28AC2B-C86A-4ED9-9537-457AB776CEBE&name=phoneName
	----------------------------------------------------
	login : 类似于 UUID. 经检测, 服务器不检测其正确性, 可以随意伪造.
	name  : 设备名称.
	device: iOS | Android | WP

 **Response:**
 	
 	{
    	"status": 0,
	    "msg": "success.",
  		"data": {
        	"user_credentials": "5UQI3c2P7pQq1PsUX74P"
    	}
	}
	--------------------------------------------------
	user_credentials: 凭证. 可用于注册华数机顶盒.
	

### 已绑定的设备列表

**Request:**

	 http://rc.weitv.me/api/v3/user_stb/list?user_credentials=itLlJ7Ij8rKq4VRDtUyZ
	 
Response:

	{
    "status": 0,
    "msg": "success.",
    "data": {
        "stb_list": [{
            "id": 12755,
            "name": "父母家",
            "stb_id": 809,
            "user_id": 49125,
            "stb": {
                "area_id": null,
                "auth_code": "",
                "created_at": "2013-08-21T09:01:17+08:00",
                "deleted_at": null,
                "hsd": "HD",
                "id": 809,
                "name": null,
                "open_id": "1000148042",
                "platform": "2",
                "playback_format": "H264",
                "profile": "HZ-NEW-SCENARIO",
                "qrcode_id": null,
                "region_id": "hzdq",
                "site_code": "hzvsite",
                "site_id": "hzvsite",
                "stb_ability": null,
                "stb_id": "1104004091900024C1481D9A",
                "stb_type": null,
                "stb_version": null,
                "updated_at": "2013-08-21T15:39:14+08:00",
                "user_id": "80493205"
            	}
        	}]
    	}
	}
	
	--------------------------------------------------------
	stb_list : 设备列表, 数组.
	name     : 被绑定设备的名称, 在手机上可显示.
	stb      : HuaSu TV Box ?
	open_id  : 设备 ID
	stb_id   :
	user_id  :
	

### 绑定设备

**Request:**

	stb_name	客厅
	user_credentials	itLlJ7Ij8rKq4VRDtUyZ
	stb_qrcode
	{
		"open_id":"1000148042",
		"resource_no":"1104004091900024C1481D9A",
		"other_param":
			"site_id:hzvsite|user_id:80493205|profile:HZ-NEW-SCENARIO|
			region_id:hzdq|	hsd:HD|playback_format:H264|			site_code:hzvsite",
		"qrcode_id":"1700148042"
	}


**Response:**

	{
    	"status": 0,
    	"msg": "success.",
    	"data": {
        	"id": 12755,
	        "name": "客厅",
    	    "stb_id": 809,
        	"user_id": 49125,
	        "stb": {
    	        "area_id": null,
        	    "auth_code": "",
            	"created_at": "2013-08-21T09:01:17+08:00",
            	"deleted_at": null,
	            "hsd": "HD",
    	        "id": 809,
        	    "name": null,
            	"open_id": "1000148042",
	            "platform": "2",
    	        "playback_format": "H264",
        	    "profile": "HZ-NEW-SCENARIO",
            	"qrcode_id": null,
	            "region_id": "hzdq",
    	        "site_code": "hzvsite",
        	    "site_id": "hzvsite",
            	"stb_ability": null,
	            "stb_id": "1104004091900024C1481D9A",
    	        "stb_type": null,
        	    "stb_version": null,
            	"updated_at": "2013-08-21T15:39:14+08:00",
	            "user_id": "80493205"
    	    }
	    }
	}

### 认证

**Request 1:**
	
	http://rc.weitv.me/api/v3/xmpp/auth?action=1&id=809&user_credentials=itLlJ7Ij8rKq4VRDtUyZ
	
**Response 1:**
	
	{
    	"status": 0,
	    "msg": "success.",
    	"data": {
        	"rlt": "0",
	        "jid": "itllj7ij8rkq4vrdtuyz@bj-xmpp02.wasu.cn/1000148042",
    	    "passwd": "123456",
        	"domain": "bj-xmpp02.wasu.cn"
    	}
	}
	
	------------------------------------------------
	jid: user_credentials@host/open_id


**Request 2:**

	http://rc.weitv.me/api/v3/xmpp/auth?action=2&id=809&user_credentials=itLlJ7Ij8rKq4VRDtUyZ
	
**Response 2:**
	
	{
    	"status": 0,
	    "msg": "success.",
    	"data": {
        	"rlt": "0",
	        "jid": "1104004091900024c1481d9a@125.210.132.146/1000148042",
	        "passwd": "",
    	    "domain": "125.210.132.146"
    	}
	}


### 距离

**Request:**

	http://recode.ditu.aliyun.com/dist_query?l=30.211111,120.011111
	
**Response:**

	{"report":0,"ad_code":"330106","dist”:””}
	
### 在电视上观看

**Request:**

	XMPP/XML Destination: 123.103.22.86:5222
	
	<message type="chat" to="1104004091900024c1481d9a@125.210.132.146/1000148042”>

	<body>
	{"header":{"time":"2014-01-2415:19:44","mid":"f19190da","opcode":"remoteCtrl","mtype":"req"},"body":{"key":"CHANNEL","param":"87”}}
	</body>

	</message>

### 电视截屏

**Request:**

	http://rc.weitv.me/api/v3/conf_stb/image.json?stb_id=809&user_credentials=itLlJ7Ij8rKq4VRDtUyZ

**Response:**

	{
		"status":0,
		"msg":"success.",
		"data":{
			"stb":"/system/confs_images/5200a35d3e21abc82b000008/58a0c7b4030946aa63f2793af749558025487456.png?1375773533”
		}
	}
	-----------------------------------------------------------
	stb: 当前电视截屏 http://rc.weitv.me/{stb}
	



## 流程



## 总结
