---
title: Método CreateObject (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d220a9abc0e2dc72d7ab65306b514a9925b4fc43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281057"
---
# <a name="createobject-method-rds"></a>Método CreateObject (RDS)
Cria o proxy para o objeto de negócios de destino e retorna um ponteiro para ele. Os pacotes e realizar marshaling dos dados de proxy para o stub do lado do servidor para comunicações com o objeto de negócios enviar solicitações e dados pela Internet. Para objetos de componente do processo, sem os proxies são usados, apenas um ponteiro para o objeto é fornecido.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 Serviço de dados remoto dá suporte aos seguintes protocolos: HTTP, HTTPS (HTTP sobre Secure Socket Layer), DCOM e em processo.  
  
|Protocol|Sintaxe|  
|--------------|------------|  
|HTTP|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|HTTPS|Set object = DataSpace.CreateObject("ProgId", "https\://awebsrvr")|  
|DCOM|Set object = DataSpace.CreateObject("ProgId", "computername")|  
|Em processo|Set object = DataSpace.CreateObject("ProgId", "")|  
  
## <a name="parameters"></a>Parâmetros  
 *Objeto*  
 Uma variável de objeto que é avaliada como um objeto que é o tipo especificado na *ProgID*.  
  
 *DataSpace*  
 Uma variável de objeto que representa um [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto usado para criar uma instância do novo objeto.  
  
 *ProgID*  
 Um **cadeia de caracteres** valor que contém o identificador programático especificando um objeto de negócios do lado do servidor que implementa as regras de negócio do seu aplicativo.  
  
 *awebsrvr* ou *computername*  
 Um **cadeia de caracteres** valor que representa uma URL que identifica o servidor Web de serviços de informações da Internet (IIS) no qual uma instância do objeto de negócios do servidor é criada.  
  
## <a name="remarks"></a>Comentários  
 O *protocolo HTTP* é o protocolo padrão da Web; *HTTPS* é um protocolo seguro da Web. Use o *protocolo DCOM* ao executar uma rede de área local sem HTTP. O *em processo* protocolo é uma biblioteca de vínculo dinâmico (DLL) local; ele não usa uma rede.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateObject (VBScript), o método de consulta e objeto DataFactory](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [Exemplo do método CreateObject (VBScript) e objeto DataSpace](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [Método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


