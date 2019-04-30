---
title: Acessar itens do servidor de relatório com acesso à URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a345cd609c4cfd79f9e93a2b63e71bbddde36ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233562"
---
# <a name="access-report-server-items-using-url-access"></a>Acessar itens de servidor de relatório com acesso à URL
  Este tópico descreve como acessar itens do catálogo de tipos diferentes em um relatório de dados do servidor de base ou em um site do SharePoint usando *rs: Command*=*valor*.  
  
 Não é necessário adicionar essa cadeia de caracteres do parâmetro. Se você omiti-lo, o servidor de relatório avalia o tipo de item e seleciona o valor do parâmetro apropriado automaticamente. No entanto, usando o *rs: Command*=*valor* cadeia de caracteres na URL melhora o desempenho do servidor de relatório.  
  
 Observação o `_vti_bin` sintaxe do proxy nos exemplos a seguir. Para obter mais informações sobre como usar a sintaxe do proxy, consulte [URL Access Parameter Reference](url-access-parameter-reference.md).  
  
## <a name="access-a-report"></a>Acessar um relatório  
 Para exibir um relatório no navegador, use o *rs: Command*=*renderizar* parâmetro. Por exemplo:  
  
 `Native` `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  É importante incluir a URL a `_vti_bin` sintaxe do proxy para encaminhar a solicitação por meio do SharePoint e o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proxy HTTP. O proxy adiciona qualquer contexto à solicitação HTTP, contexto que é necessário para garantir a execução adequada do relatório para servidores de relatório de modo do SharePoint.  
  
## <a name="access-a-resource"></a>Acessar um recurso  
 Para acessar um recurso, use o *rs: Command*=*GetResourceContents* parâmetro. Se o recurso for compatível com o navegador, como uma imagem, ele é aberto no navegador. Caso contrário, você precisará abrir ou salvar o arquivo ou recurso em disco.  
  
 `Native` `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>Acessar uma fonte de dados  
 Para acessar uma fonte de dados, use o *rs: Command*=*GetDataSourceContents* parâmetro. Se o navegador dá suporte a XML, a definição de fonte de dados é exibida se você for um usuário autenticado com `Read Contents` permissão na fonte de dados. Por exemplo:  
  
 `Native` `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 A estrutura XML pode ser semelhante ao exemplo a seguir:  
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 A cadeia de caracteres de conexão é retornada com base na **SecureConnectionLevel** configuração do servidor de relatório. Para obter mais informações sobre o **SecureConnectionLevel** , consulte [usando métodos de serviço da Web seguros](report-server-web-service/net-framework/using-secure-web-service-methods.md).  
  
## <a name="access-the-contents-of-a-folder"></a>Acessar o conteúdo de uma pasta  
 Para acessar o conteúdo de uma pasta, use o *rs: Command*=*GetChildren* parâmetro. Uma página de navegação de pasta genérica é retornada que contém links para as subpastas, relatórios, fontes de dados e recursos na pasta solicitada. Por exemplo:  
  
 `Native` `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 A interface do usuário que você vê é semelhante ao usado do modo de procura do diretório [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Server (IIS). O número de versão, incluindo o número de build, do servidor de relatório também é exibido abaixo da listagem de pastas.  
  
## <a name="see-also"></a>Consulte também  
 [Acesso à URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Referência de parâmetro de acesso à URL](url-access-parameter-reference.md)  
  
  
