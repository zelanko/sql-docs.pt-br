---
title: "Método CreateObject (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba9c2d9ee2c2cf0a646155e5d184640d1aa0283b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="createobject-method-rds"></a>Método CreateObject (RDS)
Cria o proxy para o objeto de negócios de destino e retorna um ponteiro para ele. Os pacotes e lê dados de proxy para o stub do lado do servidor para comunicação com o objeto de negócios enviar solicitações e dados pela Internet. Para objetos de componente em andamento, sem os proxies são usados, apenas um ponteiro para o objeto é fornecido.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 Serviço de dados remoto suporta os seguintes protocolos: HTTP, HTTPS (HTTP sobre SSL), DCOM e em processo.  
  
|Protocolo|Sintaxe|  
|--------------|------------|  
|HTTP|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "http://awebsrvr")|  
|HTTPS|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "https://awebsrvr")|  
|DCOM|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "computername")|  
|Em processo|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "")|  
  
## <a name="parameters"></a>Parâmetros  
 *Objeto*  
 Uma variável de objeto que é avaliada como um objeto que é o tipo especificado em *ProgID*.  
  
 *Espaço de dados*  
 Uma variável de objeto que representa um [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto usado para criar uma instância do novo objeto.  
  
 *ProgID*  
 Um **cadeia de caracteres** valor que contém o identificador programático especificando um objeto comercial do lado do servidor que implementa as regras de negócio do aplicativo.  
  
 *awebsrvr* ou *computername*  
 Um **cadeia de caracteres** valor que representa uma URL que identifica o servidor Web de serviços de informações da Internet (IIS) em que uma instância do objeto de negócios do servidor é criada.  
  
## <a name="remarks"></a>Remarks  
 O *protocolo HTTP* é o protocolo padrão da Web; *HTTPS* é um protocolo da Web seguro. Use o *protocolo DCOM* ao executar uma rede de área local sem HTTP. O *em processo* protocolo é uma biblioteca de vínculo dinâmico (DLL) local; ele não usa uma rede.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto DataFactory, método de consulta e exemplo de método CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [Exemplo de método CreateObject (VBScript) e o objeto de espaço de dados](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


