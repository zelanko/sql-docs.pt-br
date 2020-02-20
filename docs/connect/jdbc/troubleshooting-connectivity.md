---
title: Solucionar problemas de conectividade | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: bfba0b49-2e1f-411d-a625-d25fad9ea12d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d6a64589b44de50328aa3384a51e29e0c2cc9a6e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027625"
---
# <a name="troubleshooting-connectivity"></a>Solução de problemas de conectividade
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] exige que o TCP/IP esteja instalado e em execução para se comunicar com o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para verificar quais protocolos de biblioteca de rede estão instalados.  
  
 Uma tentativa de conexão de banco de dados pode falhar por muitas razões. Podem incluir o seguinte:  
  
-   O TCP/IP não está habilitado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o servidor ou número da porta especificados estão incorretos. Verifique se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando com TCP/IP no servidor e na porta especificados. Isso pode ser relatado com uma exceção semelhante a: "O logon falhou. A conexão TCP/IP ao host falhou". Isso pode ser uma das seguintes situações:  
  
    -   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi instalado, mas o TCP/IP não foi instalado como um protocolo de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Network Utility da [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior.  
  
    -   O TCP/IP foi instalado como um protocolo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas não está escutando na porta especificada na URL de conexão JDBC. A porta padrão é 1433, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser configurado durante a instalação do produto para escutar em qualquer porta. Verifique se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando na porta 1433. Ou, se a porta foi alterada, verifique se a porta especificada na URL de conexão do JDBC corresponde à porta alterada. Para obter mais informações sobre URLs de conexão do JDBC, confira [Criar a URL de conexão](../../connect/jdbc/building-the-connection-url.md).  
  
    -   O endereço do computador que é especificado na URL de conexão do JDBC não se refere a um servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado e é iniciado.  
  
    -   A operação de rede de TCP/IP entre o cliente e o servidor que executa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está funcionando. Você pode verificar a conectividade de TCP/IP com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando telnet. Por exemplo, no prompt de comando, digite `telnet 192.168.0.0 1433`, em que 192.168.0.0 é o endereço do computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e 1433 é a porta na qual ele está escutando. Se você receber uma mensagem dizendo que "O Telnet não pode se conectar", isso significa que o TCP/IP não está escutando naquela porta para conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Network Utility da [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior para ter certeza de que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja configurado para usar o TCP/IP na porta 1433.  
  
    -   A porta que é usada pelo servidor não foi aberta no firewall. Isto inclui a porta que é usada pelo servidor ou, opcionalmente, a porta associada com uma instância nomeada do servidor.  
  
-   O nome do banco de dados especificado está incorreto. Verifique se você está fazendo logon em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] existente.  
  
-   O nome de usuário ou senha está incorreta. Verifique se você tem os valores corretos.  
  
-   Quando você usa autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o JDBC Driver exige que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja instalado com autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que não é o padrão. Verifique se esta opção estará incluída quando você instalar ou configurar sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Confira também  
 [Diagnosticando problemas com o JDBC Driver](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)   
 [Conectando ao SQL Server com o JDBC Driver](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
  
  
