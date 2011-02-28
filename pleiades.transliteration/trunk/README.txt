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
  
Zeugma in English

  >>> name = u'Zeugma'
  >>> transliterate_name('en', name)
  'Zeugma'
  
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
    
