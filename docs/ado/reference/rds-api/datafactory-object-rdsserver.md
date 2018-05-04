---
title: Objeto DataFactory (RDSServer) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35918fe661c3148cd3b2962f69975ea9925a6b05
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="datafactory-object-rdsserver"></a>Objeto DataFactory (RDSServer)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Esse objeto de negócios do lado do servidor padrão implementa métodos que fornecem acesso a dados de leitura/gravação para fontes de dados especificado para aplicativos do lado do cliente.  
  
 O **RDSServer.DataFactory** objeto é criado como um objeto de automação do lado do servidor que recebe solicitações de cliente. Em uma implementação de Internet, ele reside em um servidor Web e é instanciado pelo componente ADISAPI. O **RDSServer.DataFactory** objeto fornece leitura e acesso de gravação de dados especificado fontes, mas não contém qualquer lógica de regras de validação ou business.  
  
 Se você usar um método que está disponível em ambos os **RDSServer.DataFactory** e [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objetos, o serviço de dados remoto usa o **RDS. DataControl** versão por padrão. O padrão pressupõe um cenário de programação básico, onde o **RDSServer.DataFactory** serve como um objeto genérico comercial do lado do servidor.  
  
 Se você quiser que seu aplicativo Web para tratar o processamento do lado do servidor específicos da tarefa, você pode substituir o **RDSServer.DataFactory** com um objeto comercial personalizado.  
  
 Você pode criar objetos de negócios do lado do servidor que chamam o **RDSServer.DataFactory** métodos, como [consulta](../../../ado/reference/rds-api/query-method-rds.md) e [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md). Isso é útil se você quiser adicionar funcionalidade aos objetos de negócios, mas aproveitar tecnologias existentes do serviço de dados remoto.  
  
 O **DataFactory** objeto não é seguro para scripts que são executados no lado do cliente.  
  
 A ID de classe para o **RDSServer.DataFactory** objeto é 9381D8F5-0288-11 D 0-9501-00AA00B911A5.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


