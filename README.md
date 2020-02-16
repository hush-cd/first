# first
```
import requests
import re

def gethttp(url):
    try:
        cookie = 'isg=BDEx749LyLKQ8WS5mEAf4PBEQrvLHqWQ0e8PxxNG__gXOlGMW2xuYNMYWE5c6T3I; l=cBrQ6VEnqHJszZdQKOfCPurza779UIR04kPzaNbMiICPOvfH5tMPWZU4d28MCn1Vp6pyR3-cLlaJBeYBcsYbooj62j-la; uc1=cookie14=UoTaH0A2MbIanQ%3D%3D&lng=zh_CN&cookie16=UIHiLt3xCS3yM2h4eKHS9lpEOw%3D%3D&existShop=false&cookie21=WqG3DMC9Fb5mPLIQo9kR&tag=8&cookie15=VFC%2FuZ9ayeYq2g%3D%3D&pas=0; JSESSIONID=683B79103D7BE88870810CF8BD35B9FC; hng=CN%7Czh-CN%7CCNY%7C156; mt=ci=7_1; thw=cn; _cc_=VT5L2FSpdA%3D%3D; cookie2=15ddb020a6c2337daf2069a6c103806e; csg=4db80b82; dnk=tb65622253; enc=I7%2FK9k2mtle0ZtbQ7zWarUil7Mc3ZqZz2H%2B2rySKB%2BTDsZicLUz%2BTGwQje8K%2FungF%2BP4%2BC3NnW6%2ByJ4pWPEB9g%3D%3D; existShop=MTU2Nzc1ODk2NQ%3D%3D; lgc=tb65622253; skt=bcf7828ef6c2d620; t=447b31a7e4570590dd4bdf7a105757db; tg=0; tracknick=tb65622253; uc3=nk2=F5RDKXMQcZhhGw%3D%3D&id2=UNk3CdmvjaCrdw%3D%3D&lg2=URm48syIIVrSKA%3D%3D&vt3=F8dByuPa1ivpkZsrTvQ%3D; uc4=nk4=0%40FY4I6gd8vv%2Ft9WPbN9mtl8LtMhcT&id4=0%40Ug49sy%2B1lw%2Flo9L%2Btoxe%2FUkBBxHM; alitrackid=login.taobao.com; lastalitrackid=login.taobao.com; v=0; _tb_token_=e57e57b13a6e7; _m_h5_tk=351823c8ede1ec149b5ecd787ec35973_1567441690488; _m_h5_tk_enc=14d3dfb298824350c0edad616ff7d594; cna=ugn0FRBEq34CAdvv48bqd6Yq'
        kv = {'cookie': cookie, 'user-agent': 'Mozilla/5.0'}
        r = requests.get(url, headers = kv, timeout = 30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return ''

def parserpage(ils, html):
    try:
        plt = re.findall(r'\"view_price\"\:\"[\d\.]*\"', html)
        tlt = re.findall(r'\"raw_title\"\:\".*?\"', html)
        for i in range(len(plt)):
            price = eval(plt[i].split(':')[1])
            title = eval(tlt[i].split(':')[1])
            ils.append([price, title])
    except:
            ils.append(['12', '12'])

def printGoodList(ils):
    tplt = "{:4}\t{:6}\t{:16}"
    print(tplt.format("序号", "价格", "商品名称"))
    count = 0
    for g in ils:
        count += 1
        print(tplt.format(count, g[0], g[1]))

def main():
    goods = '书包'
    depth = 2
    start_url = 'https://s.taobao.com/search?q=' + goods
    infolist = []
    for i in range(depth):
        try:
            url = start_url + '&s=' + str(44*i)
            html = gethttp(url)
            parserpage(infolist, html)
        except:
            print("error")
    printGoodList(infolist)
    #print(infolist)

main()
```
