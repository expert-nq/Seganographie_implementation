from PIL import Image
def stegano(name_img , msg):
    
    
    im = Image.open(name_img)
    
    .
    # on récupère les dimensions de l'image
    w , h = im.size
    
    
    # on sépare l'image en trois : rouge, vert et bleu
    r , g , b = im.split()
    
    
    # on transforme la partie rouge en liste
    r = list( r.getdata() )
    print("Les valeurs de R de l'image originale de 0 a 20 \n", r[0:20])
     
    
    # on calcule la longueur de la chaîne et on la transforme en binaire
    u = len(msg)
    v = bin( u )[2:].rjust(8,"0")
    print("\nLa valeur  de la longueur de la clé en binaire \n", v)
    
    
    # on transforme la chaîne en une liste de 0 et de 1 
    ascii = [ bin(ord(x))[2:].rjust(8,"0") for x in msg ]

    print("Le message claire en binaire \n",ascii[0:30])

    
    # transformation de la liste en chaîne
    a = ''.join(ascii)
    
    
    
    # on code la longueur de la liste dans les 8 premiers pixels rouges
    for j in range(8):
        r[j] = 2 * int( r[j] // 2 ) + int( v[j] )    
    
    print("\nOn stocke la longueur dans les 8 premiers pixels rouges ", r[0:8])
    
    
    
    # on code la chaîne dans les pixels suivants
    for i in range(8*u):
        r[i+8] = 2 * int( r[i+8] // 2 ) + int( a[i] )
    
    print("\nOn stocke la chaine dans les pixels suivants [8 : 8*",u,"] ", r[8:8*u])

   
    
    
    # on recrée l'image rouge 
    nr = Image.new("L",(16*w,16*h))
    nr = Image.new("L",(w,h))
    nr.putdata(r)
    
    
    # fusion des trois nouvelles images
    imgnew = Image.merge('RGB',(nr,g,b))
    
    r , g , b = imgnew.split()
    r = list( r.getdata() )
    print(r[0:8])
    
    
    print("\n Stéganalyse \n ")
    
    
    # lecture de la longueur de la chaine
    p = [ str(x%2) for x in r[0:8] ]
    q = "".join(p)
    q = int(q,2)
    print("Extraire a longueur de la chaîne en binaire  ",p)
    print("\nExtraire a longueur de la chaîne en binaire ",q)
    
    # lecture du message
    n = [ str(x%2) for x in r[8:8*(q+1)] ]
    b = "".join(n)
    message = ""
    for k in range(0,q):
        l = b[8*k:8*k+8]
        message += chr(int(l,2))
        
    print("\nle message est : ",message)
    
    
