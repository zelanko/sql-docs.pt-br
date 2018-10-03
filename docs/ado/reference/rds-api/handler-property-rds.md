---
title: Propriedade Handler (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 038cb740cd2d8e2457f83f829c85f4d6598b9f97
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824074"
---
# <a name="handler-property-rds"></a>Propriedade Handler (RDS)
Indica o nome de um programa de personalização do lado do servidor (manipulador) que estende a funcionalidade dos [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)e os parâmetros usados pelo *manipulador*.  
  
 **Aplica-se a:** [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Cadeia de caracteres*  
 Um **cadeia de caracteres** valor que contém o nome do manipulador e os parâmetros, todos separados por vírgulas (por exemplo, `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>Comentários  
 Esta propriedade dá suporte à [personalização](../../../ado/guide/remote-data-service/datafactory-customization.md), uma funcionalidade que exija configuração o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade a ser **adUseClient**.  
  
 O nome do manipulador e seus parâmetros, se houver, são separados por vírgulas (","). Um comportamento imprevisível ocorrerá se um ponto e vírgula (";") é exibido em qualquer lugar dentro do *cadeia de caracteres*. Você pode escrever seu próprio manipulador, desde que ele dá suporte a **IDataFactoryHandler** interface.  
  
 O nome do manipulador padrão é **MSDFMAP. Manipulador**, e seu parâmetro padrão é um arquivo de personalização chamado **MSDFMAP. INI**. Use essa propriedade para invocar os arquivos de personalização alternativo criados pelo administrador do servidor.  
  
 A alternativa à configuração de **manipulador** é de propriedade para especificar um manipulador de parâmetros e na [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade; ou seja, "**manipulador = * * * handlerName, parameter1, parameter2,...;* ".  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Handler (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


