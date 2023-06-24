# Lab6.2
# 1. Install Docker Desktop for Windows
    a. Ensure the following Windows Features are turned on:
      1. Virtual Machine Platform
      2. Windows Hypervisor Platform
      3. Windows Subsystem for Linux
# 2. Open Powershell and pull freeradius image
    a. PS> docker pull freeradius/freeradius-server
# 3. Build freeradius container
    a. PS> docker run -d --name freeradius -p 1812:1812:/udp -p 1813:1813/udp freeradius/freeradius-server
# 4. Copy freeradius files to local directory on host machine
    a. Identify container ID or name
      1. PS> docker ps
    b. Copy files to local directory
      2. PS> docker cp freeradius:/etc/freeradius <host path>
# 5. Open the following freeradius configuration files using Notepad++ and make changes according to Lab6.2
      1. clients.conf
      2. users
      3. dictionary
      4. sites-available/default
# 6. Build new image using updated configuration files
    a. PS> docker build . -t gamco6
# 7. Build new container using latest image
    a. PS> docker run -d --name freeradius -p 1812:1812/udp -p 1813:1813/udp gamco6
# 8. Test new server with radtest 
    a. PS> docker run -it --rm --network container:freeradius gamco6 radtest gamco2 pinchebadger localhost 0 badger docker
# 9. Download flaskapp build and use Notepad++ to change .py file to match radius secret located in freeradius clients.conf
# 10. Build new flaskapp image
    a. PS> docker build . -t newflask
# 11. Build flaskapp container with new iamge
    a. docker run -d --name newflask-contain -p 5000:5000/tcp newflask
# 12. Run the following containers in order
      1. freeradius
      2. newflask-contain
# 13. Access localhost:5000 within Edge and login using username and password created in freeradius authorize file
    a. "Welcome, gamco2" should be displayed in browser.
    
      
      
