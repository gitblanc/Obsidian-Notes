- Get all the info of your operating system
````
hostnamectl
````
- Get the content of a .sh:
````
file file.sh
````
- Get the PATH:
````
echo $PATH
````
- Get the bash functions available:
````
declare -F
````
- To count the results:
````
declare -f | wc -l
````
- List a function definition:
````
type quote
````
- Use a funtion:
````
quote bob
````
- If you don't have Internet, try this:
````
sudo ifconfig eth0 up
sudo dhclient eth0
````