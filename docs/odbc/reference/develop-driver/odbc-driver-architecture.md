---
title: Arquitetura do Driver ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d123bdf1ea3357a4846a223c41950c952c1af2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915531"
---
# <a name="odbc-driver-architecture"></a>Arquitetura do driver ODBC
Gravadores de driver devem estar cientes de que a arquitetura do driver pode afetar se um aplicativo pode usar o SQL específicas do DBMS.  
  
 ![Mostra a arquitetura do driver ODBC](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Drivers baseados em arquivo](../../../odbc/reference/file-based-drivers.md)  
  
 Quando o driver acessa os dados físicos diretamente, o driver atua como fonte de dados e do driver. O driver deve processar chamadas ODBC e instruções SQL. Os desenvolvedores de drivers baseados em arquivo devem escrever seus próprios mecanismos de banco de dados.  
  
 [Drivers baseados em DBMS](../../../odbc/reference/dbms-based-drivers.md)  
  
 Quando um mecanismo de banco de dados separado é usado para acessar os dados físicos, o driver processa somente as chamadas ODBC. Ele passa instruções SQL para o mecanismo de banco de dados para processamento.  
  
 [Arquitetura de rede](../../../odbc/reference/network-example.md)  
  
 Configurações de arquivo e o DBMS ODBC podem existir em uma única rede.  
  
 [Outras arquiteturas do driver](../../../odbc/reference/other-driver-architectures.md)  
  
 Quando um driver é necessária para trabalhar com uma variedade de fontes de dados, ele pode ser usado como o middleware. Arquitetura de mecanismo de junção heterogêneo pode fazer com que o driver aparecem como um Gerenciador de driver. Drivers também podem ser instalados em servidores, em que eles possam ser compartilhados por uma série de clientes.  
  
 Para obter mais informações sobre a arquitetura de driver, consulte [Gerenciador de Driver](../../../odbc/reference/the-driver-manager.md) e [arquitetura de Driver](../../../odbc/reference/driver-architecture.md) na seção [arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter mais informações sobre problemas de driver podem ser encontradas nas localizações descritas na tabela a seguir.  
  
|Problema|Tópico|Location|  
|-----------|-----------|--------------|  
|Problemas de compatibilidade com aplicativos e drivers|[Compatibilidade de aplicativo/Driver](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Considerações sobre programação](../../../odbc/reference/develop-app/programming-considerations.md), na referência do programador de ODBC|  
|Drivers ODBC de gravação|[Gravando drivers 3.x ODBC](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Considerações sobre programação](../../../odbc/reference/develop-app/programming-considerations.md), na referência do programador de ODBC|  
|Diretrizes de driver para compatibilidade com versões anteriores|[Diretrizes de driver para compatibilidade com versões anteriores](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Apêndice g: Diretrizes de driver para compatibilidade com versões anteriores](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), na referência do programador de ODBC|  
|Conectar-se a um driver|[Escolhendo uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[Conectar-se aos dados de um fonte ou Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), na referência do programador de ODBC|  
|Identificação de drivers|[Exibindo drivers](../../../odbc/admin/viewing-drivers.md)|[Exibindo Drivers](../../../odbc/admin/viewing-drivers.md), na Ajuda online do administrador de fonte de dados do Microsoft ODBC|  
|Habilitando o pooling de conexão|[Pooling de Conexão ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[Conectar-se aos dados de um fonte ou Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), na referência do programador de ODBC|  
|Problemas de driver e conexão Unicode/ANSI|[Drivers Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)|[Considerações sobre programação](../../../odbc/reference/develop-app/programming-considerations.md), na referência do programador de ODBC|  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
