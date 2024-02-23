# AntBuildEx03_MyBatis

## 1.	목표

build.xml의 동작 과정에 관해 이해하기 위해 이전에 했던 MyBatis 예제를 antbuild를 통해 수행한다. 

## 2.	build.xml 코드

```
<project name="ShellScriptBuilder" default="buildShellScript">

    <property name="jar.dir" value="libs"/>
    <property name="jdbc.url" value="jdbc:mysql://192.168.1.98:3306/exampledb"/>
    <property name="jdbc.user" value="user2"/>
    <property name="jdbc.password" value="Dkfvk!@234"/>

    <!-- Build shell script -->
    <target name="buildShellScript">
        
        <echo file="example_script.sh"><![CDATA[
            Creating shell script...
            #!/bin/bash

            # Get current directory of the script
            DIR="$( cd "$( dirname "${BASH_SOURCE[0]}" )" &> /dev/null && pwd )"

            DAEMON_HOME=$DIR
            DAEMON_LIB_PATH=$DAEMON_HOME/lib
            DAEMON_CLASSPATH=

            for LIB_NAME in `ls $DAEMON_LIB_PATH | grep jar`; do
                DAEMON_CLASSPATH=$DAEMON_CLASSPATH$DAEMON_LIB_PATH"/"$LIB_NAME":"
            done
        	
        	for LIB_NAME in `ls $DAEMON_LIB_PATH | grep so`; do
        	        DAEMON_CLASSPATH=$DAEMON_CLASSPATH$DAEMON_LIB_PATH"/"$LIB_NAME":"
        	done


            echo "DAEMON_HOME :: "$DAEMON_HOME
            echo "DAEMON_CLASSPATH :: "$DAEMON_CLASSPATH

            # SQL queries
            echo 'SELECT * FROM users;' | mysql -h 192.168.1.98 -P 3306 -u user2 -pDkfvk!@234 exampledb
            echo 'select xdb_enc("normal", "123123123123");' | mysql -h 192.168.1.98 -P 3306 -u user2 -pDkfvk!@234 exampledb
            echo 'select xdb_dec("normal", "AAERAAQVd0qL31mTUi9F5p2ybZS5f+3seIk=");' | mysql -h 192.168.1.98 -P 3306 -u user2 -pDkfvk!@234 exampledb
            echo 'select asg_enc("blue", "123123123123");' | mysql -h 192.168.1.98 -P 3306 -u user2 -pDkfvk!@234 exampledb
            echo 'select asg_dec("blue", "HzECAAAAAgFBU0cDAQMQAo6tey/55W7uso76JuDwRn8=");' | mysql -h 192.168.1.98 -P 3306 -u user2 -pDkfvk!@234 exampledb

            # Changing permission
            chmod 755 example_script.sh

            echo "Shell script created successfully."
        ]]></echo>
    </target>

</project>
```

## 3.	코드 설명 
	<property>엔트를 통해 라이브러리 디렉토리, jdbc url, 사용자 이름, 비밀번호를 설정한다.
	<target> 엔트를 통해 실행할 작업을 정의한다. 
	<echo>엔트를 통해 파일로 출력하도록 정의한다. 
	스크립트 파일은 bash에서 실행될 수 있도록한다.
	스크립트는 현재 스크립트 파일의 디렉토리를 찾아 DAEMON_HOME에 저장한다.
	또한 클래스 PATH를 정의한 후 암호화 및 복호화 쿼리를 실행한다.
4.	실행결과
 
5.	프로그램 실행을 통해 ANTBUILD가 동작하는 방식에 관한 이해가 늘었다. 하지만 당초에 설정했던 목표를 얻지 못했다. 
