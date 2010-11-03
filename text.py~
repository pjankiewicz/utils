# -*- coding: utf-8 -*-
import re
import string
import os

def nopolish(s):
    raw_data = s.replace(u"ł","l")    
    raw_data = raw_data.replace(u"Ł","l")
    try:
        import unicodedata        
        raw_data = unicodedata.normalize ('NFKD', raw_data).encode ('ASCII', 'ignore')
    except:
        pass
    return rawdata

def slugify(s):
    raw_data = s.replace(u"ł","l")    
    raw_data = raw_data.replace(u"Ł","l")
    try:
        import unicodedata        
        raw_data = unicodedata.normalize ('NFKD', raw_data).encode ('ASCII', 'ignore')
    except:
        pass
    output = re.sub(r'[^a-z0-9-]+', '-', raw_data.lower()).strip('-')
    return re.sub(r'-+', '-', output)

def split_multi(text,splits=[";",","]):
    for k in splits[1:]:
	text = text.replace(k,splits[0])
    return text.split(splits[0])
    
def hashit(s):
    from hashlib import sha256
    return sha256(settings.SALT + s).hexdigest()
    
PL_UNIT_GRAMMAR = {
	"badge":("odznak","odznaka","odznaki"),
	"answer":("odpowiedzi","odpowiedź","odpowiedzi"),
	"vote":("głosów","głos","głosy"),
	"view":("odsłon","odsłona","odsłony"),
	"point":("punktów","punkt","punkty"),
	"tag":("tagów","tag","tagi"),
	"question":("pytań","pytanie","pytania"),
	"user":("użytkowników","użykownik","użytkowników"),
	"people":("osób","osoba","osoby"),
	"hour":("godzin","godzina","godziny"),
	"day":("dni","dzień","dni"),
	"week":("tygodni","tydzień","tygodnie"),
	"month":("miesięcy","miesiąc","miesiące"),
	"year":("lat","rok","lata"),
	"comment":("komentarzy","komentarz","komentarze"),
	"containing":("zawierających","zawierające","zawierające"),
}

def pl_units(word,number):
    if number <= 0:
        return PL_UNIT_GRAMMAR[word][0]
    if number == 1:
        return PL_UNIT_GRAMMAR[word][1]
    mod = number % 10
    if mod >= 2 and mod <= 4 and (number > 20 or number < 10):
        return PL_UNIT_GRAMMAR[word][2]
    return PL_UNIT_GRAMMAR[word][0]
    

def wordbreak (string, arg, html = True):
    """
    funkcja ktora dzieli dlugie slowa
    """
    search = '([^ ]{' + str(arg) + '})'
    wbr = "@!@#$!@#.to_dzieli_slowa"
    saferesult = (re.sub( search, '\\1' + wbr, string ))
    if html:
        result = saferesult.replace(wbr,'&shy;')
    else:
        result = saferesult.replace(wbr,' ')
    return result

def firsttoupper(input):
    if len(input)==1:
	    return input.upper()
    else:
	    return input[0].upper() + input[1:]

def auto_link(text):
    """Make links for urls in plain text. Ported from http://snippets.dzone.com/posts/show/7455"""
    generic_URL_regexp = re.compile( r'(?P^|[\n ])(?P[\w]+?://[\w]+[^ \"\n\r\t<]*)', re.I | re.M )
    starts_with_www_regexp = re.compile( r'(?P^|[\n ])(?P(www)\.[^ \"\t\n\r<]*)', re.I | re.M )
    starts_with_ftp_regexp = re.compile( r'(?P^|[\n ])(?P(ftp)\.[^ \"\t\n\r<]*)', re.I | re.M )
    email_regexp = re.compile( r'(?P^|[\n ])(?P[a-z0-9&\-_\.]+?)@(?P[\w\-]+\.([\w\-\.]+\.)*[\w]+)', re.I )

    s = text or ''
    s = str(s)

    s = generic_URL_regexp.subn(r'\g<a href="\g">\g', s)[0]
    s = starts_with_www_regexp.subn(r'\g<a href="http://\g">\g', s)[0]
    s = starts_with_ftp_regexp.subn(r'\g<a href="ftp://\g">\g', s)[0]
    s = email_regexp.subn(r'\g<a href="mailto:\g@\g">\g@\g', s)[0]
    return s
