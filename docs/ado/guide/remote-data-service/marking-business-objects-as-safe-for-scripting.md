---
title: Marcando objetos de negócios como seguros para script | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 729daea7fe719f33ec8931424143c3fedc5ac86f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62675919"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>Marcar objetos de negócios como seguros para script
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para ajudar a garantir um ambiente seguro de Internet, você precisa marcar todos os objetos comerciais instanciados com o [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) do objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) o método como "seguro para script". Você precisa garantir que eles são marcados como tal na área de licença do registro do sistema antes que possam ser usados no DCOM.  
  
> [!NOTE]
>  Marcado como "seguro para script" ou para inicialização de objetos de negócios podem ser instanciados e inicializados por qualquer pessoa na rede. Marcar um objeto comercial "seguros para script" torna segura. É extremamente importante garantir que os objetos comerciais são codificados com o maior nível de segurança para garantir que esses objetos não apresentam um ponto de acesso desprotegido para dados confidenciais.  
  
 Para marcar manualmente seu objeto de negócios como seguros para script, crie um arquivo de texto com uma extensão. reg que contém o texto a seguir. Neste exemplo, \< *MyActiveXGUID*> é o número GUID hexadecimal do seu objeto de negócios. Os seguintes dois números habilitar o recurso de seguro para execução de scripts:  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 Salve o arquivo e mesclá-lo ao seu registro usando o Editor do registro ou duas vezes no arquivo. reg no Windows Explorer.  
  
 Objetos de negócios criados no Microsoft Visual Basic podem ser marcados automaticamente como "seguros para script" com o Assistente de implantação e pacote. Quando o assistente pede que você especifique as configurações de segurança, selecione **seguras para inicialização** e **seguros para script**.  
  
 Na última etapa, o Assistente de instalação do aplicativo cria um arquivo. htm e um arquivo. cab. Você pode, em seguida, copie esses dois arquivos ao computador de destino e clique duas vezes no arquivo. htm para carregar a página e registrar corretamente o servidor.  
  
 Porque o objeto comercial será instalado no diretório Windows\System32\Occache por padrão, mova-o para o diretório Windows\System32 e alterar o **HKEY_CLASSES_ROOT\CLSID\\**  \< *MyActiveXGUID*>\\**InprocServer32** chave do registro para coincidir com o caminho correto.


