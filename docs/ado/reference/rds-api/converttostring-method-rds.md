---
description: Método ConvertToString (RDS)
title: Método ConvertTostring (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: rothja
ms.author: jroth
ms.openlocfilehash: ec87fd4bc4495874aae88b3051081e30dda9bbb9
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722422"
---
# <a name="converttostring-method-rds"></a>Método ConvertToString (RDS)
Converte um [conjunto de registros](../ado-api/recordset-object-ado.md) em uma cadeia de caracteres MIME que representa os dados do conjunto de registros.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataFactory*  
 Uma variável de objeto que representa um objeto [RDSServer. datafactory](./datafactory-object-rdsserver.md) .  
  
 *Recordset*  
 Uma variável de objeto que representa um objeto **Recordset** .  
  
## <a name="remarks"></a>Comentários  
 Com arquivos. asp, use **ConvertToString** para inserir o **conjunto de registros** em uma página HTML gerada no servidor para transportá-lo para um computador cliente.  
  
 **ConvertToString** primeiro carrega o **conjunto de registros** nas tabelas de serviço de cursor e, em seguida, gera um fluxo no formato MIME.  
  
 No cliente, o Remote Data Service pode converter a cadeia de caracteres MIME de volta em um **conjunto de registros**totalmente funcional. Ele funciona bem para lidar com menos de 400 linhas de dados com, no máximo, 1024 bytes de largura por linha. Você não deve usá-lo para transmitir dados de BLOB e conjuntos de resultados grandes por HTTP. Nenhuma compactação de transmissão é executada na cadeia de caracteres, de modo que conjuntos de dados muito grandes demorarão um tempo considerável para transporte por HTTP quando comparado ao formato tablegram otimizado para fio definido e implantado pelo serviço de dados remoto como seu formato de protocolo de transporte nativo.  
  
> [!NOTE]
>  Se você estiver usando Active Server páginas para inserir a cadeia de caracteres MIME resultante em uma página HTML do cliente, lembre-se de que versões do VBScript anteriores à versão 2,0 limitam o tamanho da cadeia de caracteres a 32K. Se esse limite for excedido, um erro será retornado. Mantenha o escopo da consulta relativamente pequeno ao usar a inserção de MIME por meio de arquivos. ASP. Para corrigir isso, baixe a versão mais recente do VBScript no site do Microsoft Windows Script Technologies.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataFactory (RDSServer)](./datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método ConvertTostring (VB)](../ado-api/converttostring-method-example-vb.md)   
 [Exemplo do método ConvertToString (VBScript)](./converttostring-method-example-vbscript.md)