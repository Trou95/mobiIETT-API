# MobiIETT API
Otobüsüm Nerede(Mobiiett) servisinin bulunan endpoint listesi.

<hr>

## Auth

    

> URL: ntcapi.iett.istanbul
> 
> Endpoint: oauth2/v2/auth

**Request:**

	{
		client_id: string;
		client_secret: string;
		grant_type: string; 
		scope: string;
	}

> client_id: Cihaz kimliği
> 
> client_secret: Cihaz için atanan secret key
> 
> grant_type: autharization tipi ("client_credentials" olarak belirtilmeli)
> 
> scope: Oluşturulacak token'in kullanılacağı scope (sonraki isteklerde gerekli olacak. "service" olarak belirtilmeli)


 

> **Not**: client_id & client_secret bilgileri cihaz için uygulamanın kurulum aşamasında oluşturuluyor. Kontrolünün nasıl sağlandığından emin değilim. Uzun süre önce oluşturduğum bilgilerle giriş yapabiliyorum.

**JS ve Axis ile örnek bir Request**

    {
     "client_id":"thAwizrcxoSgzWUzRRzhSyaiBQwQlOqA",
     "client_secret":"jRUTfAItVHYctPULyQFjbzTyLFxHklykujPWXKqRntSKTLEr",
     "grant_type":"client_credentials",
     "scope":  "service"
    }

**Response:**

    {
    	access_token: string;
    	token_type: string;
    	expires_in: number; 
    	refresh_token: string;
    	expire_date: string;
    }

<hr>

    const axios = require('axios');


    const apiUrl = 'https://ntcapi.iett.istanbul/oauth2/v2/auth'; // Değiştirmeniz gereken URL
    
    const requestBody = {
      client_id: 'thAwizrcxoSgzWUzRRzhSyaiBQwQlOqA',
      client_secret: 'jRUTfAItVHYctPULyQFjbzTyLFxHklykujPWXKqRntSKTLEr',
      grant_type: 'client_credentials',
      scope: 'service'
    };
    
    axios.post(apiUrl, requestBody)
      .then(response => {
        console.log('Access Token:', response.data.access_token);
      })
      .catch(error => {
        console.error('Hata:', error.response ? error.response.data : error.message);
      });


<hr>

## Arama

> Endpoint: /service
> 
> alias: mainGetLine_basic_search

**Request**

    {
	    alias: string;
	    data: object
    }

**Örnek Request & Response**

    {
	    "alias": "mainGetLine_basic_search",
	    "data": {
		    "HATYONETIM.HAT.HAT_KODU":"%50%D%"
	    }
    }

<hr>

    [
	    {   
		    "HAT_HAT_ADI":  "AYAZAĞA - ALİBEYKÖY",   
		    "HAT_HAT_KODU":  "50D",
		    "HAT_HAT_TIPI":  10,
		    "HAT_ID":  3601
	    }
    ]

## Rota Bilgisi

> Endpoint: /service
> 
> alias: mainGetRoute

**Örnek Request & Response**

    {
	    "alias":"mainGetRoute",   
	    "data":{
		    "HATYONETIM.GUZERGAH.YON":"119",
		    "HATYONETIM.HAT.HAT_KODU":"50D" 
	    }
    }

<hr>

    [
	    {
		    "HAT_HAT_KODU":  "50D",
		    "HAT_ID":  3601,
		    "GUZERGAH_DEPAR_NO":  0,
		    "GUZERGAH_GUZERGAH_KODU":  "50D_G_D0",
		    "GUZERGAH_YON":  119,
		    "GUZERGAH_SEGMENT_SIRA":  1,
		    "DURAK_ADI":  "AYAZAĞA",
		    "DURAK_DURAK_KISA_ADI":  "301751",
		    "DURAK_DURAK_KODU":  301751,
		    "DURAK_GEOLOC":  {
			    "x":  29.0013410055968,
			    "y":  41.1227419915094
		    },
		    "DURAK_ID":  293812,
		    "DURAK_YON_BILGISI":  "SON DURAK",
		    "ILCELER_ILCEADI":  "Sarıyer",
		    "ILCELER_TUIK_ILCE_KODU":  1604
	    },
	    {
		    "HAT_HAT_KODU":  "50D",
		    "HAT_ID":  3601,
		    "GUZERGAH_DEPAR_NO":  0,
		    "GUZERGAH_GUZERGAH_KODU":  "50D_G_D0",
		    "GUZERGAH_YON":  119,
		    "GUZERGAH_SEGMENT_SIRA":  1,
		    "DURAK_ADI":  "BLOKLAR- ŞEHİT MEHMET CİVAK",
		    "DURAK_DURAK_KISA_ADI":  "115731",
		    "DURAK_DURAK_KODU":  115731,
		    "DURAK_GEOLOC":  {
			    "x":  28.9994669645928,
			    "y":  41.1220159650117
		    },
		    "DURAK_ID":  293929,
		    "DURAK_YON_BILGISI":  "LEVENT",
		    "ILCELER_ILCEADI":  "Sarıyer",
		    "ILCELER_TUIK_ILCE_KODU":  1604
	    },
	    ...
    ]

## Hat Bilgisi

> Endpoint: /service
> 
> alias: mainGetBusRunBusStopPass

    {
	    alias: string;
	    data : object {
	    AKYOLBILYENI.H_GOREV.GOREVDURUMID: string;
	    AKYOLBILYENI.H_GOREV.HATID: string;
    }

<hr>
    
> Endpoint: /service
> 
> alias: mainGetLine_basic
  
     {  
		alias: string,  
		 data: object {
		    HATYONETIM.GUZERGAH.YON: string;
		    HATYONETIM.HAT.HAT_KODU: string;
		 }
    }
        
 <hr>
 
> Endpoint: /service
> alias: mainGetLiveBus_basic
  
  

     {
    	alias: string;
    	data: object {
	    	AKYOLBILYENI.K_GUZERGAH.HATID: number
	    }
    }

## Duyuru

> Endpoint: /service
> 
> alias: ybs

    {
	  alias: string;
	  data: object {
		  data: object {
			  password: string;
			  username: string;
			 },
		}
		method: string,
		path: string[]
	 }

> **Not**: username ve password sabit değerlere sahip.
> 
> username: netuce
> 
> password: n1!t8c7M1

**Örnek Request & Response**

    {
	    "alias":"ybs",
	    "data":{
		    "data":{
			    "password":"n1!t8c7M1",
			    "username":"netuce"
		    },
		    "method":"POST",
		    "path":[
			    "real-time-information",
			    "line-status",
			    "55",
			    "*"
		    ]
		}
    }

<hr>

   ![Response](https://i.hizliresim.com/88meqrb.png)
