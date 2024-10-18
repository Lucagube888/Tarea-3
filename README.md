
<h2>1- Realiza unha consulta "dig danielcastelao.org" e identific cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER- SECTION, AUTHORITY SECTION, etc)</h2>

    dig danielcastelao.org
    
Neste caso, non aparece unha AUTHORITY SECTION na resposta, o que significa que non se están devolvendo servidores autoritativos nesta resposta directa. Isto pode ocorrer se o teu servidor DNS cachea a resposta e non necesita consultar a un servidor autoritativo.
Noutras circunstancias, esta sección indicaría os servidores de nomes autoritativos para o dominio, que son os que conteñen a información oficial sobre o dominio.


<h2>2- Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org</h2> 
    
    dig moodle.danielcastelao.org
    
En header a diferenza é o ide do NXDOMAIN, Non hai ANSWER SECTION na saída para esta consulta. Isto é porque, como o dominio non existe ou non ten un rexistro para configurado, non se pode devolver unha dirección IP e en AUTHORITY SECTION Nesta sección, podes ver os servidores autoritativos responsables deste dominio.

<h2>3- Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?</h2>

    dig ns danielcastelao.org
    
O nome dos servidores DNS son ns2.hover.com e ns1.hover.com, para obter o seu ip hai que poñer o comando dig A ns1.hover.com , dig A ns2.hover.com, a ip de ns1.hover.com é 216.40.47.26, e a ip de ns2.hover.com  é 64.98.148.13. . Xeralmente, téñense polo menos dous servidores autoritativos para garantir redundancia e dispoñibilidade no caso de que un falle, Redundancia: Se un dos servidores falla ou se atopa inaccesible, o outro pode seguir respondendo as consultas. 

<h2>4- Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.</h2>

    dig -x 130.206.164.68

Asi coas outras dous IP.

<h2>5- A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?</h2>

Para saber que servidor DNS estou a usar uso o comando cat /#etc/resolv.conf.
Podes cambiar o servidor DNS temporalmente nunha consulta dig usando: 

    dig @8.8.8.8 danielcastelao.org


<h2>6- Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org.</h2> 

Para consultar o rexistro SOA ao servidor de Google:

    dig @8.8.8.8 SOA moodle.danielcastelao.org, 

logo para consultar ao servidor primario do dominio: 

    dig @<ns1.hover.com> SOA moodle.danielcastelao.org,

<h2>7- Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?</h2>

Para consultar a IP de www.elpais.com, usamos o comando: 

    dig www.elpais.com

El TTL son 23 segundos, y queda almacenado 23 segundos hasta que llegue a cero, momento en el cual se volverá a hacer la consulta a un servidor DNS autoritativo.

<h2>8- Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?</h2>

Neste caso use a pagina de eneba e pccomponentes:

    dig www.eneba.com
    
    dig www.pccomponentes.com


As diferenzas nos valores de TTL débense ás necesidades específicas do servizo en canto a abalo de carga, dispoñibilidade, seguridade e eficiencia de rede.

<h2>9- Determina o TTL máximo (original) dun nome de dominio.</h2>

Neste caso vin o TTL de google, o que hize para ver, o TTL maximo foi usar o comando repetidamente ata ver o maximo:

    dig www.google.com
   
<h2>10- Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?</h2>

    dig www.google.com A

Se, hai multiples IPs. As IPs detrás dun dominio como www.google.es non sempre son as mesmas nin aparecen no mesmo orde debida a un proceso chamado abalo de carga e distribución xeográfica. Google usa diferentes servidores en distintos lugares para manexar o tráfico, e o DNS rota as direccións IP para distribuír o traballo de maneira equitativa entre eles.

<h2>11- Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo</h2>

    dig j.roostserver.net
    
    dig -x 3.33.243.145
    
    dig -x 15.197.204.56
    
O servidor se acepta o modo recursivo. Cando poño o comando dig -x coas ip do servidor que apareces ao poñer un dig j.rootserver.net as ip devolven aviso.


<h2>12- Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados</h2>

    dig +trace www.timesonline.co.uk
    
Estas son todas as consultas DNS do servidor raíz ata o servidor que ten a resposta final. Dominio www.timesonline.co.uk está a apuntar a tres  direccións IP.

<h2>13- Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org</h2>

    dig danielcastelao.org MX
    
Estas son as direccións de correo en orde de prioridade do dominio danielcastelao.org 



<h2>14- Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?</h2>

    dig www.facebook.com AAAA
    
Se o dominio ten rexistros AAAA, a resposta amosará os enderezos IPv6 asociados. Estes enderezos son utilizados para acceder a www.facebook.com a través da rede IPv6 en lugar da tradicional IPv4.
