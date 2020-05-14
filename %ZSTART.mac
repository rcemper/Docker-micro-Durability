%ZSTART ; for docker demo by RCC 2020-05-11
	quit
SYSTEM
	for user="_system","superuser" {
		set s=##class(Security.Users).%OpenId(user)
			,s.ChangePassword=0
			,sc=s.%Save()
	}
	set s=##class(Security.Users).%OpenId("unknownuser")
			,sc=s.Roles.Insert("%All")
			,sc=s.%Save()
	quit
LOGIN
	quit
JOB
	quit
CALLIN
	quit	
