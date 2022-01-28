# yamlbasics
**This repository contains useful information on YAML syntax**
YAML is a superset of JSON. Which means any valid JSON file is also a valid YAML file.

YAML has two basic structures.
  . Lists
  . Maps


## YAML Maps:
Maps lets you associate Key/name and value pairs.

```
 apiVersion : v1
 kind : Pod
```

an equivalent JSON representaton is 

```
{
"apiVersion": "v1",
"kind" : "Pod"
}
```

## Maps with in Maps:
```
apiVersion: v1
kind: Pod
metadata:
  name: rss-site
  lables:
    app: web
```
here, we can see that the key metadata has its value in the form of an another map with two more keys , name and lables. also, the lables key intern has another map as its value with a key names map.

While the YAML processor cares about intendation it doesnt matter if we use one space or several spaces, as long as we use those spaces consistently when we create keyvalue pairs, maps and lists. we probably should avoid using tab space.

## YAML LIsts:
YAML lists are simply a sequence of object.

```
fruits:
   - apple
   - orange
   - grapes
   - mango
 ```
 YAML lists can have any number of items in them. 
 
 JSON equivalent for the above code would be:
 ```
 {
  "fruits": ["apple","organce", "Grapes", " mango"]
 }
 ```
 ## Maps with in Lists:
 YAML lists can have maps as its elements.
 
 ```
 apiVersion: v1
 kind: Pod
 metadata:
   name: rss-site
   lables:
     app:web
  spec:
    containers:
      - name: font-end
        image: nginx
        ports:
          - containerPort: 80
       - name: rss-reader
         image: nkaruman/rss-php-nginx:v1
         ports:
           - containerPort: 88
 ```
 
 here, we can see a list of container obhects each of which contains a name, image and a list of ports.
 
 ## summary: 
 . YAML Maps are a groupd of Name/key - value pairs.
 . lists are individual items.
 . maps of maps
 . maps of lists
 . lists of lists
 . lists of maps
**Note: Github markup reference link**
https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
