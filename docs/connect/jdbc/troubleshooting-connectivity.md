---
title: Solucionando problemas de conectividade | Microsoft Docs
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
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b213cb9d2a3527b967afef5dc28aa11d82fd0f9d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshooting-connectivity"></a>Solucionando problemas de conectividade
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] requer que o TCP/IP esteja instalado e em execução para se comunicar com seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados. Você pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] do Configuration Manager para verificar quais protocolos de biblioteca de rede estão instalados.  
  
 Uma tentativa de conexão de banco de dados pode falhar por muitas razões. Eles podem incluir o seguinte:  
  
-   TCP/IP não está habilitado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], ou o servidor ou número de porta especificado está incorreto. Verifique [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está escutando com TCP/IP no servidor especificado e porta. Isto poderia ser relatado com uma exceção semelhante a: "O logon falhou. A conexão TCP/IP ao host falhou". Isso pode ser uma das seguintes situações:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está instalado, mas TCP/IP não tiver sido instalado como um protocolo de rede para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Network Utility da [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de configuração de [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] e posterior.  
  
    -   TCP/IP é instalado como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] protocolo, mas ele não está escutando na porta especificada na URL de conexão JDBC. A porta padrão é 1433, mas [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] pode ser configurado durante a instalação do produto para escutar em qualquer porta. Verifique se [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está escutando na porta 1433. Ou, se a porta foi alterada, verifique se a porta especificada na URL de conexão do JDBC corresponde à porta alterada. Para obter mais informações sobre URLs de conexão JDBC, consulte [criar a URL de Conexão](../../connect/jdbc/building-the-connection-url.md).  
  
    -   O endereço do computador que está especificado na conexão do JDBC URL não faz referência a um servidor onde [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é instalado e iniciado.  
  
    -   A operação de rede de TCP/IP entre o cliente e o servidor que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] não está funcionando. Você pode verificar a conectividade TCP/IP para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando telnet. Por exemplo, no prompt de comando, digite `telnet 192.168.0.0 1433` onde 192.168.0.0 é o endereço do computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e 1433 é a porta que ele está escutando. Se você receber uma mensagem informando que "O Telnet não pode se conectar", o TCP/IP não está escutando naquela porta para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conexões. Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Network Utility da [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de configuração de [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] e posterior para ter certeza de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para usar TCP/IP na porta 1433.  
  
    -   A porta que é usada pelo servidor não foi aberta no firewall. Isto inclui a porta que é usada pelo servidor ou, opcionalmente, a porta associada com uma instância nomeada do servidor.  
  
-   O nome do banco de dados especificado está incorreto. Certifique-se de que você está fazendo logon em um existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.  
  
-   O nome de usuário ou senha está incorreta. Verifique se você tem os valores corretos.  
  
-   Quando você usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, o JDBC driver exige que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] é instalado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, que não é o padrão. Certifique-se de que essa opção estiver incluída quando você instalar ou configurar sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Diagnosticar problemas com o Driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
