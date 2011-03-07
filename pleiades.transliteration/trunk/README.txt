-*- encoding: utf-8 -*-

Copyright 2009, 2010 Institute for the Study of the Ancient World, New York
University

Introduction
============

This package provides modules for transliteration of names from Greek and Latin
writing systems into our modern Roman writing system following conventions of
the Classical Atlas Project.

Examples:

  >>> from pleiades.transliteration import transliterate_name
    
Roma in Latin 
    
  >>> transliterate_name('la', 'Roma')
  'Roma'
    
Choma in Greek with Latin transliteration (pretend it's ancient!)
    
  >>> transliterate_name('grc-latn', 'Choma')
  'Choma'
    
Aphrodisias in Greek
    
  >>> name = u'\u1f08\u03c6\u03c1\u03bf\u03b4\u03b5\u03b9\u03c3\u03b9\u03b5\u03cd\u03c2'
  >>> transliterate_name('grc', name)
  'Aphrodeisieus'

Aphrodisiensis in Greek characters (no accents)
    
  >>> name = u'\u1f08\u03c6\u03c1\u03bf\u03b4\u03b9\u03c3\u03b9\u03b5\u03bd\u03c3\u03b9\u03c2'
  >>> transliterate_name('la-grek', name)
  'Aphrodisiensis'
  
all characters in English

  >>> name = u'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ.()'
  >>> transliterate_name('en', name)
  'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ.()'
  
all characters in Turkish
  >>> name = u'ABC\u00c7DEFG\u011eHI\u0130JKLMNO\u00d6PRS\u015eTU\u00dcVYZ abc\u00e7defg\u011fh\u0131ijklmno\u00f6prs\u015ftu\u00fcvyz.()'
  >>> transliterate_name('tr', name)
  'ABCCDEFGGHIIJKLMNOOPRSSTUUVYZ abccdefgghiijklmnooprsstuuvyz.()'
  
all characters in Coptic
  >>> name = u'\u03E2\u03E3\u03E4\u03E5\u03E6\u03E7\u03E8\u03E9\u03EA\u03EB\u03EC\u03ED\u03EE\u03EF\u2C80\u2C82\u2C84\u2C86\u2C88\u2C8C\u2C8E\u2C90\u2C92\u2C94\u2C96\u2C98\u2C9A\u2C9C\u2C9E\u2CA0\u2CA2\u2CA4\u2CA6\u2CAA\u2CAC\u2CAE\u2CB0\u03E2\u03E3\u03E4\u03E5\u03E6\u03E7\u03E8\u03E9\u03EA\u03EB\u03EC\u03ED\u03EE\u03EF\u2C81\u2C83\u2C85\u2C87\u2C89\u2C8D\u2C8F\u2C91\u2C93\u2C95\u2C97\u2C99\u2C9B\u2C9D\u2C9F\u2CA1\u2CA3\u2CA5\u2CA7\u2CAB\u2CAD\u2CAF\u2CB1\u2CEF\u2CF0\u2CF1'
  >>> transliterate_name('cop', name)
  'SHshFfKHkhHhJjQqTItiABGDEZETHIKLMNXOPRSTPHCHPSOSHshFfKHkhHhJjQqTItiabgdezethiklmnxoprstphchpso'

  >>> name = 'ⲙⲛⲧⲣⲙⲛⲕⲏⲙⲉ'.decode('utf-8')
  >>> transliterate_name('cop', name)
  'mntrmnkeme'

Zeugma in Greek

  >>> name = u'\u0396\u03b5\u1fe6\u03b3\u03bc\u03b1'
  >>> transliterate_name('grc', name)
  'Zeugma'
  
Zeugma in Latin

  >>> name = u'Zeugma'
  >>> transliterate_name('la', name)
  'Zeugma'

Invalid script

  >>> transliterate_name('tlh', 'kitten') # doctest: +ELLIPSIS
  Traceback (most recent call last):
  ...
  ValueError: Unsupported writing system (tlh)
    
Editorial characters that should be permitted

  >>> transliterate_name('la', '(...)sinsensium')
  '(...)sinsensium'

Out-of-range characters that shouldn't be there if the validator was used 
first. Aphrodisias in Greek but mis-languaged as latin
    
  >>> name = u'\u1f08\u03c6\u03c1\u03bf\u03b4\u03b9\u03c3\u03b9\u1f71\u03c2'
  >>> transliterate_name('la', name.encode('utf-8'))
  '??????????'
    
