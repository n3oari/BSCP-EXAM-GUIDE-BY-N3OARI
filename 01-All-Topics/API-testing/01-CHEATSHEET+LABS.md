# API Testing - CHEATSHEET + MOST IMPORTANT LABS

## Key Terms

```
- Burp Extension -> Content-Type Converter
```

## Walkthrough - Most Important Labs

[Finding-and-exploiting-an-unused-API-endpoint](Finding-and-exploiting-an-unused-API-endpoint.md)

[Exploiting-a-mass-assignament-vulnerability-(hidden-parameter-fields)](Exploiting-a-mass-assignament-vulnerability-(hidden-parameter-fields).md)

## Methodology

[api-wordlist-repo-by-chrislockard](https://github.com/chrislockard/api_wordlist)

```
- Recon ->
	  > Search in official api documentacion (different versions too)
	  > /api + Sitemap
	  > Site map -> Engagement tools -> discover content
	  > Burp Intruder ->
	   	  > Add HTTP verbs list in critical endpoints
	   	  > /api/<wordlist> 
	   	  > /api/<version>/<wordlist/
	  > Content-Type: json/xml? -> Content-Type-Converter -> see changes
```

