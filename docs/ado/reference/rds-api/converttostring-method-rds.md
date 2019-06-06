---
title: Método ConvertToString (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e88823d01e34a18bebe209f3939f8cb3532530f4
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712310"
---
# <a name="converttostring-method-rds"></a>Método ConvertToString (RDS)
Converte um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) para uma cadeia de caracteres MIME que representa os dados do conjunto de registros.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataFactory*  
 Uma variável de objeto que representa um [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Recordset*  
 Uma variável de objeto que representa um **Recordset** objeto.  
  
## <a name="remarks"></a>Comentários  
 Com arquivos. asp, use **ConvertToString** inserir os **conjunto de registros** em uma página HTML gerada no servidor para transportá-lo para um computador cliente.  
  
 **ConvertToString** carregado pela primeira vez o **Recordset** no serviço do Cursor tabelas e, em seguida, gera um fluxo no formato MIME.  
  
 No cliente, o serviço de dados remoto pode converter a cadeia de caracteres MIME em um plenamente **conjunto de registros**. Ele funciona bem para lidar com as linhas de menos de 400 dos dados com não mais do que a largura de 1024 bytes por linha. Você não deve usá-lo para o fluxo de dados BLOB e grandes conjuntos de resultados via HTTP. Nenhuma compactação durante a transmissão é executada a cadeia de caracteres muito grandes conjuntos de dados levará um tempo considerável para transportar via HTTP quando comparado com o formato de otimização de transmissão tablegram definidos e implantados pelo serviço de dados remoto como seu formato de protocolo de transporte nativo.  
  
> [!NOTE]
>  Se você estiver usando o Active Server Pages para inserir a cadeia de caracteres MIME resultante em uma página HTML de cliente, lembre-se de que as versões anteriores à versão 2.0 do VBScript limitam o tamanho da cadeia de caracteres para 32 mil. Se esse limite for excedido, um erro será retornado. Mantenha o escopo da consulta relativamente pequeno ao usar a inserção de MIME por meio de arquivos. ASP. Para corrigir isso, baixe a versão mais recente do VBScript no site Microsoft Windows Script tecnologias.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método ConvertToString (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [Exemplo do método ConvertToString (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


