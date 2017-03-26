#!/bin/bash

. hooks/config

#set -e
while [ -e Temp/UnityLockFile ]
do
	echo I cannot build while the project is still open in Unity. I will wait 5 seconds and try again.
	sleep 5
done

echo "running tests"
set -e
"$MSBuildLocation" tests/KusoTest/KusoTest.sln
"$MSTestLocation" /testcontainer:tests/KusoTest/KusoTest/bin/Debug/KusoTest.dll

echo "executing build"
"$unityLocation" -batchmode -quit -projectpath $projectFolder -buildTarget Android $workingFolder/windows/$projectName/$projectName.exe

hooks/butler push $workingFolder/android/$projectName $itchURL:android$1
echo "pushed!"