---
title: Conectando-se a um banco de dados SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49645b1f-39b1-4757-bda1-c51ebc375c34
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7e7452a001f96b38b8e2a6047a144a82b5f957a9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-to-an-azure-sql-database"></a>Conectando-se a um banco de dados SQL do Azure
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Este tópico aborda problemas ao usar o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] para se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)]. Para obter mais informações sobre como conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], consulte:  
  
-   [SQL Database do Azure](http://go.microsoft.com/fwlink/?LinkID=202490)  
  
-   [Como: conectar-se ao SQL Azure usando JDBC](http://msdn.microsoft.com/library/gg715284.aspx)  
  
-   [Usando o SQL Azure em Java](http://msdn.microsoft.com/library/windowsazure/hh749029(VS.103).aspx)

-   [Conectar-se usando a Autenticação do Azure Active Directory](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)  
  
## <a name="details"></a>Detalhes  
 Ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], você deve se conectar ao banco de dados mestre para chamar **GetCatalogs**.  
 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] não oferece suporte a retornar o conjunto inteiro de catálogos de um banco de dados do usuário. **GetCatalogs** usa a exibição de sys. Databases para obter os catálogos. Consulte a discussão de permissões em [sys. Databases (banco de dados do SQL Azure)](http://go.microsoft.com/fwlink/?LinkId=217396) entender **GetCatalogs** comportamento em um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)].  
  
 Conexões removidas  
 Ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], conexões ociosas podem ser finalizadas por um componente de rede (como um firewall) após um período de inatividade. Existem dois tipos de conexões ociosas nesse contexto:  
  
-   Ociosas na camada TCP, onde as conexões podem ser removidas por qualquer número de dispositivos de rede.  
  
-   Ociosas pelo SQL Azure Gateway, onde TCP **keepalive** as mensagens podem ocorrer (tornando a conexão não ociosa de uma perspectiva de TCP), mas não tinha uma consulta ativa em 30 minutos. Nesse cenário, o Gateway determina se a conexão TDS é ociosa em 30 minutos e termina a conexão.  
  
 Para evitar a remoção de conexões ociosas por um componente de rede, as configurações do Registro a seguir (ou seus equivalentes em ambientes não Windows) devem ser definidas no sistema operacional no qual o driver foi carregado:  
  
|Configuração do Registro|Valor recomendado|  
|----------------------|-----------------------|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ parâmetros \ KeepAliveTime|30000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ parâmetros \ KeepAliveInterval|1.000|  
|HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ Tcpip \ parâmetros \ TcpMaxDataRetransmissions|10|  
  
 Você deve reiniciar o computador para que as configurações do Registro tenham efeito.  
  
 Para obter esse efeito no Windows Azure, crie uma tarefa de inicialização para adicionar as chaves do Registro.  Por exemplo, adicione a tarefa de inicialização abaixo ao arquivo de definição de serviço:  
  
```  
<Startup>  
    <Task commandLine="AddKeepAlive.cmd" executionContext="elevated" taskType="simple">  
    </Task>  
</Startup>  
```  
  
 Depois adicione um arquivo AddKeepAlive.cmd file ao seu projeto. Defina a configuração "Copiar para Diretório de Saída" para Copiar sempre. A seguir, há um exemplo de arquivo AddKeepAlive.cmd:  
  
```  
if exist keepalive.txt goto done  
time /t > keepalive.txt  
REM Workaround for JDBC keep alive on SQL Azure  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveTime /t REG_DWORD /d 30000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v KeepAliveInterval /t REG_DWORD /d 1000 >> keepalive.txt  
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters /v TcpMaxDataRetransmissions /t REG_DWORD /d 10 >> keepalive.txt  
shutdown /r /t 1  
:done  
```  
  
 Anexando o nome do servidor à ID de usuário na cadeia de conexão  
 Antes da versão 4.0 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], era necessário acrescentar o nome do servidor à ID de usuário na cadeia de conexão. Por exemplo, user@servername. Começando na versão 4.0 do [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], não é mais necessário anexar @servername à ID de usuário na cadeia de conexão.  
  
 Uso de criptografia requer a configuração de hostNameInCertificate  
 Ao se conectar a um [!INCLUDE[ssAzure](../../includes/ssazure_md.md)], você deve especificar **hostNameInCertificate** se você especificar **criptografar = true**. (Se o nome do servidor na cadeia de conexão é *shortName*. *domainName*, defina o **hostNameInCertificate** propriedade \*. *domainName*.)  
  
 Por exemplo:  
  
```  
jdbc:sqlserver://abcd.int.mscds.com;databaseName= myDatabase;user=myName;password=myPassword;encrypt=true;hostNameInCertificate= *.int.mscds.com;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
