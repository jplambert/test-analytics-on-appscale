# Add local JAR

mvn install:install-file -DgroupId=com.google.code.gwt-dnd -DartifactId=gwt-dnd -Dversion=3.1.1 -Dpackaging=jar -Dfile=gwt-dnd-3.1.1.jar

# Install GAE, run in dev mode

mvn gae:unpack
mvn gae:run

# How to install AppScale Tools (used on dev side, as opposed to run side)

https://github.com/AppScale/appscale-tools/wiki/Installing-the-AppScale-Tools-on-Linux
sudo apt-get install python-pip -y
sudo pip install appscale-tools

# Local AppScale stuff

appscale init cluster
put the VM IP in the AppScaleFile --> 192.168.33.10
appscale up
