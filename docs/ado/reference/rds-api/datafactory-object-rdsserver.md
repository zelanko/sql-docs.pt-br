---
title: Objeto datafactory (RDSServer) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97597e15bc5cd8ee8d3008c97f3a4e8b07b2d43d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964321"
---
# <a name="datafactory-object-rdsserver"></a>Objeto DataFactory (RDSServer)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Esse objeto comercial padrão do lado do servidor implementa métodos que fornecem acesso de dados de leitura/gravação a fontes de dados especificadas para aplicativos do lado do cliente.  
  
 O objeto **RDSServer. datafactory** é projetado como um objeto de automação do lado do servidor que recebe solicitações do cliente. Em uma implementação da Internet, ela reside em um servidor Web e é instanciada pelo componente ADISAPI. O objeto **RDSServer. datafactory** fornece acesso de leitura e gravação a fontes de dados especificadas, mas não contém nenhuma lógica de validação ou regra de negócio.  
  
 Se você usar um método que esteja disponível no **RDSServer. datafactory** e no [RDS. Objetos DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) , o serviço de dados remotos usa o **RDS. Versão do DataControl** por padrão. O padrão pressupõe um cenário de programação básico, em que o **RDSServer. datafactory** serve como um objeto de negócios genérico do lado do servidor.  
  
 Se desejar que seu aplicativo Web manipule o processamento do lado do servidor específico da tarefa, você poderá substituir o **RDSServer. datafactory** por um objeto comercial personalizado.  
  
 Você pode criar objetos comerciais do lado do servidor que chamam os métodos **RDSServer. datafactory** , como [Query](../../../ado/reference/rds-api/query-method-rds.md) e [createrecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md). Isso será útil se você quiser adicionar funcionalidade aos seus objetos comerciais, mas aproveitar as tecnologias de serviço de dados remoto existentes.  
  
 O objeto **DataFactory** não é seguro para scripts executados no lado do cliente.  
  
 A ID de classe do objeto **RDSServer. datafactory** é 9381D8F5-0288-11D0-9501-00AA00B911A5.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método CreateObject, do método Query e objeto DataFactory (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


