---
title: Arquitetura driver ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 712de6a7a3f80ce1cd3ca854a88765dbfa531356
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294554"
---
# <a name="odbc-driver-architecture"></a>Arquitetura do driver ODBC
Os escritores de driver devem estar cientes de que a arquitetura do driver pode afetar se um aplicativo pode usar o SQL específico do DBMS.  
  
 ![Mostra a arquitetura do driver ODBC](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [Drivers baseados em arquivos](../../../odbc/reference/file-based-drivers.md)  
  
 Quando o motorista acessa os dados físicos diretamente, o motorista atua como motorista e fonte de dados. O driver deve processar tanto chamadas ODBC quanto declarações SQL. Os desenvolvedores de drivers baseados em arquivos devem escrever seus próprios mecanismos de banco de dados.  
  
 [Drivers baseados em DBMS](../../../odbc/reference/dbms-based-drivers.md)  
  
 Quando um mecanismo de banco de dados separado é usado para acessar dados físicos, o driver processa apenas chamadas ODBC. Ele passa instruções SQL para o mecanismo de banco de dados para processamento.  
  
 [Arquitetura de rede](../../../odbc/reference/network-example.md)  
  
 As configurações de Arquivo e DBMS ODBC podem existir em uma única rede.  
  
 [Outras arquiteturas do driver](../../../odbc/reference/other-driver-architectures.md)  
  
 Quando um driver é obrigado a trabalhar com uma variedade de fontes de dados, ele pode ser usado como middleware. A arquitetura heterogênea do motor pode fazer com que o motorista apareça como um gerenciador de driver. Os drivers também podem ser instalados em servidores, onde podem ser compartilhados por uma série de clientes.  
  
 Para obter mais informações sobre arquitetura de driver, consulte [Driver Manager](../../../odbc/reference/the-driver-manager.md) e [Driver Architecture](../../../odbc/reference/driver-architecture.md) na seção em [Arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Mais informações sobre problemas com motoristas podem ser encontradas nos locais descritos na tabela a seguir.  
  
|Problema|Tópico|Location|  
|-----------|-----------|--------------|  
|Problemas de compatibilidade com aplicativos e drivers|[Compatibilidade de aplicativos/drivers](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[Considerações de Programação](../../../odbc/reference/develop-app/programming-considerations.md), na Referência do Programador ODBC|  
|Escrevendo drivers ODBC|[Gravar drivers 3.x ODBC](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[Considerações de Programação](../../../odbc/reference/develop-app/programming-considerations.md), na Referência do Programador ODBC|  
|Diretrizes do driver para compatibilidade retrógrada|[Diretrizes de driver para compatibilidade com versões anteriores](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[Apêndice G: Diretrizes do Driver para Compatibilidade Retrógrada,](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)na referência do programador ODBC|  
|Conectando-se a um driver|[Escolher uma fonte de dados ou um driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[Conectando-se a uma fonte de dados ou driver,](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)na referência do programador ODBC|  
|Identificação de motoristas|[Exibir drivers](../../../odbc/admin/viewing-drivers.md)|[Exibindo drivers](../../../odbc/admin/viewing-drivers.md), na ajuda on-line do administrador de origem de dados do Microsoft ODBC|  
|Habilitando o pool de conexões|[Pooling de conexão ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[Conectando-se a uma fonte de dados ou driver,](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)na referência do programador ODBC|  
|Problemas de driver e conexão Unicode/ANSI|[Drivers Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)|[Considerações de Programação](../../../odbc/reference/develop-app/programming-considerations.md), na Referência do Programador ODBC|  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
