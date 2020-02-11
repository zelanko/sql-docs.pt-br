---
title: Arquitetura do driver ODBC | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915531"
---
# <a name="odbc-driver-architecture"></a>Arquitetura do driver ODBC
Os gravadores de driver devem estar cientes de que a arquitetura do driver pode afetar se um aplicativo pode usar o SQL específico do DBMS.  
  
 ![Mostra a arquitetura do driver ODBC](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Drivers baseados em arquivo](../../../odbc/reference/file-based-drivers.md)  
  
 Quando o driver acessa os dados físicos diretamente, o driver atua como o driver e a fonte de dados. O driver deve processar tanto chamadas ODBC quanto instruções SQL. Os desenvolvedores de drivers baseados em arquivo devem gravar seus próprios mecanismos de banco de dados.  
  
 [Drivers baseados em DBMS](../../../odbc/reference/dbms-based-drivers.md)  
  
 Quando um mecanismo de banco de dados separado é usado para acessar dados físicos, o driver processa apenas chamadas ODBC. Ele passa instruções SQL para o mecanismo de banco de dados para processamento.  
  
 [Arquitetura de rede](../../../odbc/reference/network-example.md)  
  
 As configurações de ODBC de arquivo e DBMS podem existir em uma única rede.  
  
 [Outras arquiteturas do driver](../../../odbc/reference/other-driver-architectures.md)  
  
 Quando um driver é necessário para trabalhar com uma variedade de fontes de dados, ele pode ser usado como middleware. A arquitetura do mecanismo de junção heterogênea pode fazer com que o driver apareça como um Gerenciador de driver. Os drivers também podem ser instalados em servidores, onde podem ser compartilhados por uma série de clientes.  
  
 Para obter mais informações sobre a arquitetura do driver, consulte [Gerenciador de driver](../../../odbc/reference/the-driver-manager.md) e [arquitetura de driver](../../../odbc/reference/driver-architecture.md) na seção sobre [arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Mais informações sobre problemas de driver podem ser encontradas nos locais descritos na tabela a seguir.  
  
|Problema|Tópico|Location|  
|-----------|-----------|--------------|  
|Problemas de compatibilidade com aplicativos e drivers|[Compatibilidade de aplicativo/driver](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Considerações sobre programação](../../../odbc/reference/develop-app/programming-considerations.md), na referência do programador de ODBC|  
|Gravando drivers ODBC|[Gravar drivers 3.x ODBC](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Considerações sobre programação](../../../odbc/reference/develop-app/programming-considerations.md), na referência do programador de ODBC|  
|Diretrizes de driver para compatibilidade com versões anteriores|[Diretrizes de driver para compatibilidade com versões anteriores](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Apêndice G: diretrizes de driver para compatibilidade com versões anteriores](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md), na referência do programador de ODBC|  
|Conectando a um driver|[Escolher uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[Conectando-se a uma fonte de dados ou driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), na referência do programador de ODBC|  
|Identificando drivers|[Exibir drivers](../../../odbc/admin/viewing-drivers.md)|[Exibindo drivers](../../../odbc/admin/viewing-drivers.md), na ajuda online do administrador de fonte de dados ODBC da Microsoft|  
|Habilitando o pool de conexões|[Pooling de conexão ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[Conectando-se a uma fonte de dados ou driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md), na referência do programador de ODBC|  
|Problemas de conexão e driver Unicode/ANSI|[Drivers Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)|[Considerações sobre programação](../../../odbc/reference/develop-app/programming-considerations.md), na referência do programador de ODBC|  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolver um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
