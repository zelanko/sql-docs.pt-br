---
title: Marcar objetos comerciais como seguros para script | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e9e400052e9c3cb794089d1731d42abd6feca37
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>Marcar objetos comerciais como seguros para script
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para ajudar a garantir um ambiente seguro de Internet, você precisa marcar qualquer objetos comerciais instanciados com o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) do objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método como "seguro para script". Você precisa garantir que eles são marcados como tal na área de licença do registro do sistema antes que possam ser usados em DCOM.  
  
> [!NOTE]
>  Objetos de negócios marcados como seguros para inicialização ou "seguro para script" podem ser instanciados e inicializados por qualquer pessoa na rede. Marcar um objeto comercial "seguro para script" não torná-lo seguro. É extremamente importante garantir que os objetos comerciais são codificados com o maior nível de segurança para garantir que esses objetos não apresentar um ponto de acesso desprotegido para dados confidenciais.  
  
 Para marcar manualmente o objeto comercial como seguros para script, crie um arquivo de texto com uma extensão. reg que contém o texto a seguir. Neste exemplo, \< *MyActiveXGUID*> é o número hexadecimal do GUID de seu objeto de negócios. Os seguintes dois números habilitar o recurso seguro para execução de scripts:  
  
```  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 Salve o arquivo e mesclá-lo em seu registro usando o Editor do registro ou duas vezes no arquivo. reg no Windows Explorer.  
  
 Objetos de negócios criados no Microsoft Visual Basic podem ser marcados automaticamente como "seguro para script" com o Assistente de implantação e pacote. O assistente solicita que você especifique as configurações de segurança, selecione **seguros para inicialização** e **seguros para script**.  
  
 Na última etapa, o Assistente de instalação do aplicativo cria um arquivo. htm e um arquivo. cab. Você pode copiar esses dois arquivos para o computador de destino e duas vezes no arquivo. htm para carregar a página e registrar corretamente o servidor.  
  
 Porque o objeto comercial será instalado no diretório Windows\System32\Occache por padrão, mova-o para a pasta Windows\System32 e altere o **HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32** chave do registro para coincidir com o caminho correto.


