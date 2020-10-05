---
description: Marcar objetos de negócios como seguros para script
title: Marcando objetos comerciais como seguros para scripts | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- business objects in RDS [ADO]
ms.assetid: 0be98d1a-ab3d-4dce-a166-dacda10d154a
author: rothja
ms.author: jroth
ms.openlocfilehash: 6681a0b40890db9c344a91adc26694f3e122710d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721498"
---
# <a name="marking-business-objects-as-safe-for-scripting"></a>Marcar objetos de negócios como seguros para script
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
 Para ajudar a garantir um ambiente de Internet seguro, você precisa marcar todos os objetos comerciais instanciados com o [RDS. ](../../reference/rds-api/dataspace-object-rds.md) Método [CreateObject](../../reference/rds-api/createobject-method-rds.md) do objeto DataSpace como "seguro para scripts". Você precisa garantir que eles sejam marcados como tal na área de licença do registro do sistema antes que possam ser usados no DCOM.  
  
> [!NOTE]
>  Os objetos comerciais marcados como "seguros para criação de scripts" ou seguros para inicialização podem ser instanciados e inicializados por qualquer pessoa na rede. A marcação de um objeto de negócios "seguro para scripts" não o torna seguro. É vitalmente importante garantir que os objetos comerciais sejam codificados com a segurança mais alta para garantir que esses objetos não apresentem um ponto de acesso desprotegido para dados confidenciais.  
  
 Para marcar manualmente seu objeto comercial como seguro para scripts, crie um arquivo de texto com uma extensão. reg que contenha o texto a seguir. Neste exemplo, \<*MyActiveXGUID*> é o número de GUID hexadecimal do seu objeto comercial. Os dois números a seguir habilitam o recurso seguro para scripts:  
  
```console
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]  
[HKEY_CLASSES_ROOT\CLSID\<MyActiveXGUID>\Implemented   
Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]  
```  
  
 Salve o arquivo e mescle-o no registro usando o editor do registro ou clicando duas vezes no arquivo. reg no Windows Explorer.  
  
 Os objetos comerciais criados no Microsoft Visual Basic podem ser marcados automaticamente como "seguros para criação de scripts" com o assistente de pacote e implantação. Quando o assistente solicitar que você especifique as configurações de segurança, selecione **seguro para inicialização** e **seguro para scripts**.  
  
 Na última etapa, o assistente de instalação do aplicativo cria um arquivo. htm e um. cab. Em seguida, você pode copiar esses dois arquivos para o computador de destino e clicar duas vezes no arquivo. htm para carregar a página e registrar corretamente o servidor.  
  
 Como o objeto comercial será instalado no diretório Windows\System32\Occache por padrão, mova-o para o diretório Windows\System32 e altere a chave do registro **HKEY_CLASSES_ROOT \CLSID \\ ** \<*MyActiveXGUID*> \\ **InprocServer32** para corresponder ao caminho correto.