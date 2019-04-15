/odata/write
body sql
-----------
{
	"Success":false,
	"Message":"",
	"rows":0
}

/odata/scale
body sql
------------
{
	"Success":false,
	"Message":"",
	"Scalar":0
}


/odata/get

body sql
------------
{
	"Success":false,
	"Message":"",
	"Item":{}
}

/odata/test

{
	"Success":false,
	"Message":""
}


+++++++++++++++++++++++

/odata/query/{pagesize}/{pageindex}/{pk}
body sql
---------------
{
	"Success":false,
	"Message":"",
	"Total":20,
	"PageNo":1,
	"Items"[{},{}]
}
