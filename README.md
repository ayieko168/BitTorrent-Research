# BitTorrent-Research
## My research on the BitTorrrent protoal that I plan to use in creatin a movie streaming programm

###### **Belleow are internet resources that I hve found extreemly helpfull:**

1. A Simple online byte counter
  	- UTF-8 string length & byte counter = https://mothereff.in/byte-counter#%5Cxa9%60EP%5Cxaa%5Cxe7%5Cxde%5Cx06%5Cxc8%7B%5Cxa3%5Ct%5Cx7f%5Cxdc.%5Cxf3

2. The BitTorrent Protocol Specification Site 
	- http://www.bittorrent.org/beps/bep_0003.html

3. A .torrent file decoder 
	- Torrent decode = https://www.tools4noobs.com/online_tools/torrent_decode/

	- Bencode Online = https://chocobo1.github.io/bencode_online/

4. An Article on how to build your own bittorrent client using Javascript 
	- How to make your own bittorrent client = https://allenkim67.github.io/programming/2016/05/04/how-to-make-your-own-bittorrent-client.html

5. StackOverFlow Solutions to some problems I stumbled on
	- Why my GET request to a torrent tracker doesn't work? = https://stackoverflow.com/questions/39997621/why-my-get-request-to-a-torrent-tracker-doesnt-work

	- Torrent related: tracker response on UDP protocol (Update #3 - working) = https://stackoverflow.com/questions/15184376/torrent-related-tracker-response-on-udp-protocol-update-3-working?rq=1

	- Calculating the info-hash of a torrent file = https://stackoverflow.com/questions/19749085/calculating-the-info-hash-of-a-torrent-file

6. An article on how to decode the bencode data, based on the bencode.py module. 
	He says: 
	> I've written this because bencode.py in the BitTorrent source doesn't really handle nested bencoded data found in scrapes and this 	is on average 5-6 times faster than the perl implementation
	
	Code: ```python3
	
			import re
			try:
				import psyco # Optional, 2.5x improvement in speed
				psyco.full()
			except ImportError:
				pass
			decimal_match = re.compile('\d')

			def bdecode(data):
				'''Main function to decode bencoded data'''
				chunks = list(data)
				chunks.reverse()
				root = _dechunk(chunks)
				return root

			def _dechunk(chunks):
				item = chunks.pop()

				if item == 'd': 
					item = chunks.pop()
					hash = {}
					while item != 'e':
						chunks.append(item)
						key = _dechunk(chunks)
						hash[key] = _dechunk(chunks)
						item = chunks.pop()
					return hash
				elif item == 'l':
					item = chunks.pop()
					list = []
					while item != 'e':
						chunks.append(item)
						list.append(_dechunk(chunks))
						item = chunks.pop()
					return list
				elif item == 'i':
					item = chunks.pop()
					num = ''
					while item != 'e':
						num  += item
						item = chunks.pop()
					return int(num)
				elif decimal_match.search(item):
					num = ''
					while decimal_match.search(item):
						num += item
						item = chunks.pop()
					line = ''
					for i in range(int(num)):
						line += chunks.pop()
					return line
				raise "Invalid input!"
				```
	- Decoding bencoded data with python = https://wiki.theory.org/index.php/Decoding_bencoded_data_with_python

7. The BitTorrent bencode python module 
	- a leight-weight, standalone package. = https://pypi.org/project/BitTorrent-bencode/

8. .NET library for encoding/decoding bencode and reading/writing torrent files  
	- Link = https://github.com/Krusen/BencodeNET#usage

9. A Blog on how to write your own torrent client using **clojure** programming language 
	- BitTorrent Tracker Protocol = https://nakkaya.com/2009/12/03/bittorrent-tracker-protocol/
    - clojure online comiler  =  https://repl.it/languages/clojure

10. An online utility website that has almost all conversion tools:
	- ASCII,Hex,Binary,Decimal,Base64 converter = https://www.rapidtables.com/convert/number/ascii-hex-bin-dec-converter.html

11. Online utility to convert Magnet links to .torrent file 
	- Convert a magnet link to torrent file  = http://magnet2torrent.com/
