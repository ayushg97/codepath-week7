# Project 7 - WordPress Pentesting

Time spent: **13** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

1. Unauthenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: If wordpress stored text over 64 kb in the database, it was truncated, and displaying after it was fetched from the database would not properly clean html attributes, allowing for xss.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Works < 4.2
    - Fixed in version: 4.2.1
    - DB Link - https://wpvulndb.com/vulnerabilities/7945
    - CWE-79
    - No CVE
  - [ ] GIF Walkthrough: ![](https://github.com/ayushg97/codepath-week7/blob/master/1.gif)
  - [ ] Steps to recreate: 
    - Copy and paste this text into a wordpress comment 
    - &lt;a title='x onmouseover=alert(unescape(/hello%20world/.source)) style=position:absolute;left:0;top:0;width:5000px;height:5000px  AAAAAAAAAAAA...[64 kb]..AAA'&gt;&lt;/a&gt;
    - Replace the ...[64 lb].. with any amount of data that would result in the total size of the text being over 64kb.
    - Mouseover the newly added comment to view an xss attack.
  - [ ] Affected source code:
    - https://core.trac.wordpress.org/changeset/32307/branches/4.2/src/wp-includes/wp-db.php
2. Authenticated Stored Cross-Site Scripting (XSS)
  - [ ] Summary: This takes advantage of how shortcodes are parsed by wordpress, which allows for xss injection.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Works < 4.2.3
    - Fixed in version: 4.2.3
    - DB Link - https://wpvulndb.com/vulnerabilities/8111
    - CWE-79
    - CVE 2015-5622
    - CVE 2015-5623
  - [ ] GIF Walkthrough: ![](https://github.com/ayushg97/codepath-week7/blob/master/2.gif)
  - [ ] Steps to recreate: 
    - Go to the page where you create a new post as an admin
    - Create a new post and go to text mode, and paste in
    - &lt;a href="[caption code=">]&lt;/a>&lt;a title=" onmouseover=alert('test')  ">link&lt;/a>
    - Preview the post and mouse over the text to get an xss popup
  - [ ] Affected source code:
    - https://core.trac.wordpress.org/changeset/33360/branches/4.2/src/wp-includes/shortcodes.php
3. Authenticated Shortcode Tags Cross-Site Scripting (XSS)
  - [ ] Summary: The way wordpress parsed shortcode was using a technique called KSES. This had a vulnerability which did not properly detect HTML tags, allowing for insertion of javascript, and XSS.
    - Vulnerability types: XSS
    - Tested in version: 4.2
    - Works <= 4.3
    - Fixed in version: 4.3.1
    - DB Link - https://wpvulndb.com/vulnerabilities/8186
    - CWE-79
    - CVE 2015-5714
  - [ ] GIF Walkthrough: ![](https://github.com/ayushg97/codepath-week7/blob/master/3.gif)
  - [ ] Steps to recreate:
    - Go to the page where you create a new post as an admin
    - Create a new post and go to text mode, and paste in
    - TEST!!![caption width="1" caption='&lt;a href="' ">]&lt;/a>&lt;a href="http://onMouseOver='alert(1)'">Click me&lt;/a>
    - Preview the post and mouse over the text to get an xss popup
  - [ ] Affected source code:
    - https://core.trac.wordpress.org/changeset/33499/branches/4.2
4. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
5. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets

All assets are with their associated vulnerabilities

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

## Notes

Describe any challenges encountered while doing the work.

It was hard to find how too execute vulnerabilites. The majority of items that wpscan shows do not show information about how to execute a hack. I could only really do ones with tutorial links from wpscan. This limits thet amout of vulnerabilites I could carry out and it took me a while to find ones that are reproduceable. 

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
