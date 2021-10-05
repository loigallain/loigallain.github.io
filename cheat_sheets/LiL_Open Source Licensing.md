# Open Source Licensing
https://www.linkedin.com/learning/programming-foundations-open-source-licensing/welcome?u=98011314

## what is a license?
is a permission ot undertake some activity
comes with duties and obligation
need to obey the rules
licenses is **not** a contract
a contract is a bargain for exchanges between parties. it can be 
- bilateral: a promise in exchange of a promise (e.g. purchase of house, employment contract, lease contract)
- unilateral: a promise in exchange for some action (e.g. return for a pet, only the looking for his pet is making a promise)

license has no bargain (no negociation) for exchange: there are requirements attached to the license. either one complies with those or not. If one doesn't then the authority is revoked. in the last case, you will have no liability to get a recourse (no reimbursement possible). the fact that the licenses is accepted is per say the agreement with the terms of use.

with the contract, one party cannot simply revoke the other's rights.

A license can also a permission to use and posses software/intellectual property

a software license can be a contract
depends on the terms of the EULA. it typically covers a license and an agreement (hence some contract)

## Copyright, Trademark and Patent
the one who writes the software is the copyright owner. he is allowed to use and distribute copies of the software.
it is the basic property law concept associated with the industry software
look into the Intellectual Property Fundamentals (on linked in learning) by dana Robinson
### Copyright
is the exclusive legal rigth to use, copy and distribute a creative work
work must be tangible. it must be perceived by other.
### Trademark
a word or a symbol used to describe a company, a product or a service
trademark is about branding
### Patent
is the exclusive right to make, use and/or sell an invention
yes software can be patented

what the software does when executed is subject to patent, while the code written to make the software is subjected to copyright

***All of the above can be licensed*** this is for allowing anyone else but the owner of the copyright, the trademark or the patent to use it.

## Introduction to Open Source
OSS licensing is at the intersection of Intellectual Property and Open Sources Principles that the OSS Licensing is found.
Open Source initiative is explained on OpenSource.org website.
it is more than having the code the made available, 10 factors must be there:
1. Free redistribution: license shall not restrict anyone from giving away the software to then be integrated. you can charge for the usage, not prevent the distribution
2. must provide source code or make it available
3. license must allow for derived work to be redistributed
4. the integrity of author's code must be maintained. 
5. no discrimination against person or groups
6. no discrimination against fields of endeavor
7. distribution of only one license required to secure rights
8. license must not be specific to a product (one cannot enforce the usage of a propriatory software)
9. license must not restric other software (not the entire product has to be open soruces)
10. license must be technically neutral

## Software License
is a grant of permission to use software. it may also include rights to modify and distribute the software
### simple software license
>(c) 2016 by John Doe
>Anybody is free to use the software for any purpose
is has a copyright, and defines what can be done with it. the text here specifies what can be done.

### BSD
Berkely Software Distribution **BSD**

permissive accademic class licensing
Release in 1990 by the University California Berkeley. it was a rework of the 1988 version.

First version was made of 1 paragraph. 1990's version has four paragraph. It was not recognized as "open source" license because of the clause 3.
It is therefore a permissive software license.
btw, the 3rd clause was cumbersome to maintain. As it was imposing the maintainance of an exhaustive list of users to then be advertised (by the way the advertisement clause also was the reason why this could not be open source, according to the Open Source Initiative)
The Three Clause BSD version was publish in 1999 which was removing the clause 3.

### Open Source licenses vs Public Domain
*public domain*: all intellectual property protection have lapsed. there is no need for a license. Having something part of the public domain is not removing the license. it often refers to object/software created by the government agents.

public domain nor open source are nowhere related to the fact that 
 the thing is free.

A copyright is created immediately upon creation. And hence, the copyright can never be removed (created upon creation of the object). The only way then one can legally use a software created by another is by way of license.
Hence OSS (Open Source Software) are not part of the public domain.

### GPL - Apache - MIT
GPL - GNU Public License: copyleft

Apache 2.0 is commercial permissive

MIT - Academic permissive

All are OSI approved
they all have an "as is" Disclaimer
No recourse against the project or any contributor is possible

#### GPL and other GNU Licenses
most extensive
part of the few treated as an actual license vs. a contract (because of paragraph 9)
one can do modification of the code inside the organization and never share them with the community... unless and until the software is being released/distributed! (license never mentions release, but assumption is that release and distribution are here to be treated as of equal meaning)

GPL 2 and GPL 3
Two versions of GPL are existing today.

- V3 contains compatibility guidance on how to combine software under different OSS licenses
- V3 contains specific patent grant language
- entire text can be found at http://www.gnu.org/licenses/gpl.html

in commercial context makes it complex to use because of the viral nature of the licence.
this comes from the defintion of "modify" and "covered work":
- to *modify* a work means to copy from of adapt all or part of the work in a fashion requiring copyright permission, other thant the makein of an exact copy. the resulting work is called a "modified version" ot the earlier work or a work "based on" the earlier work
- a *covered work* means either the unmodified Program or a work based on the Program

one can use a GPL code w/o accepting the terms of the license. it is only when one modifies, copies or distributes the code that there is an acceptance for the licence terms.

Distributing the GPL License
this is done by providing the license once in the source code tree and addition of a one liner for each of the source code file

funny, the GPL text itself is itself **not** open :D

#### MIT
very similar to BSD
takes its roots in university
- general disclaimer language
- is also a permissive license
- but MIT license makes it explicite that is allowed to copy, use, modify, merge, publish, distribute, sublicense or sell the software

the MIT license is completely silent as to sharing the modification made.
BSD and MIT are silent wrt to patents. should we desire to grant patent rights, the project will need a separate document

the MIT license applies to exact same copy of the software. it means that:
- if nothing is changed in the software then the license file must be added
- if there is any change made on the software, then these changes can be licensed under any different license


#### The Apache license
now at version 2
most commercial friendly one
- it has a general disclaimer language
- like GPL has a patent grant, but **without the reciprocity** and there is **no need to share the modifications**. license of each portion of the code must be clearly spelled out.
- including apache licensed code into a commercial application doesn't impact the commercial code itself
- unlike the MIT and the GPL license, the Apache has an embedded contributor license agreement (CLA) (between the project and the contributor). it is important when submitting code to the project to articulate clearly what is the status of each code, the project must ensure it has the right to use the code it receives

### Permissive vs. copyleft open-source license 
a permissive license (e.g. BSD; MIT, Apache) has a very limited set of restrictions and obligations

Copyleft (e.g. GPL family) is a play on word to copyright (right vs.left): it sdescribes an arrangment whereby a work may be used, modified and distributed freely on condition that **anything** derived from it is bound by the **same condition**.
Copyright is about the **exclusive** legal right the author has to use, copy and distribute a creative work.

With copyleft, as an author, I want to ensure that anyone has the right to copy and use my work.
GPL is the Copyleft license that comes into 2 flavors:
- GPLS v3: **strong copyleft**: combines GPL covered source code with non GPL code **does** make the target code subject to GPL
- LGPLV3: **weak copyleft** distribution of binary file binaries (dlls) **does not** affect the license of target code that references dlls (dynamic linking)

### Chossing right open-source license
one should consider the following questions:
1. if you don't care about placing any restrictions on your software, and you are not interested in what happens downstream... then go for **MIT** or alike. MIT can also work for commercial, however it doesn't content any specific language concerning copyright and patent grant nor trademark
2. if one is concerned with distribution, and wants to make sure that the code doesn't land into any proprietary software (or code), then you should proceed with the **GPL family**. Remember that you will also be shielded from the revenue generated by it (because of the reciprocical nature of the license)
3. if you want to have some commercial exploitation of your solution/code and even encourage its wider adoption, then **Apache** is the go to model. it is a permissive license that also offer patent and copyright disclaimers.

## Other topics
### Non Software Work and the Creative Commons
foudned in 2001
- used for content (non software)
- embrace the copyleft principles
- closest possibility to get something into public domain immediately
- reference on https://creativecommons.org/
e.g. licenses GPL are under CC

Attribution: every cc license requires the creator of the work to be credited
Restrictions: some may be applied as the creator sees fit
- share alike: no modification can be applied to it. symbol is reverse arrow. imposes to retain the original license terms
- non coommercial use
- no derivatives: one must take and retain the work "as is"

A license can be created from the website, the website also provide some clarity on the various combination one wants to see applied in the license

### Multiple Open-source license scenarios and compatibility

one must make that there is a compatibility accross licenses terms into a software.

### Dual Licensing
typical scenario with a EULA.
EULA allows to:
- offer access to alpha/beta version
- negotiate on more restrictive terms
- negotiate with individual customers
- offer paid support services
e.g. Red Hat Linux is based on this model which combines GPL and EULA

### Contributor license agreements
when open source project, one may have contributors. CLA makes it clear to contributor whether they are allowed to do.
Apache license is the only one having a CLA embedded into it.
implementing an explicit CLA is an absolute best practices (see example on google website)?
since it documente the provenance of all code in the projetc, the benefits of CLA:
- every contributor is warranted that he/she has the right to make the contribution
- makes it explicit that contributors are transferring copyright to project and subsequent users
- makes it explicit that contributors are transferring patent right to project and subsequent users

### the role of the patent licenses and promises
the patent license shall express the grant of all patent rights
it **cannot** be revoked
PAtent promise:
- to not enforce the patent rights
- can be revoked at any time
  
A promise is not a contract supported by consideration.
example of patent promise can be found on http://www.redhat.com/legal/patent_policy.html

### Establishing a business entity for your project
for every project, one can/must establish a business entity to support it. It can be Corporation, LLC or partnership

- it helps to shift identity of the project from the individual personalities
- it ensures some sort of life for the project that goes beyon the individuals

The most successful OSS projects treat it (the project) as a business (jQuery, Open Office, RedHat, MySQL, MongoDB, ...).

some tips for your open source project:
 - consider affiliating with some open-source foundation (like Apache, Mozilla, Outercurve)
 - have your business entity not individuals own the copyright to the project
 - establish a board and some semblance of management
 - find a corporate sponsor (e.g. Glimpse project: https://glimpse-editor.org/)

## Next steps
Reading
Intellectual Property Fundamentals, with Dana Robinson
Understanding Copyrigh: a deeper dive with Dana Robinson