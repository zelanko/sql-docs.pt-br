---
title: Configurando o RDS no Windows 2000 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
author: rothja
ms.author: jroth
ms.openlocfilehash: c5bd4829382a3724b4999e3f87de29a561bd6a29
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750071"
---
# <a name="configuring-rds-on-windows-2000"></a>Configurar o RDS no Windows 2000
Se você tiver dificuldades para que o RDS funcione corretamente após a atualização para o Windows 2000, siga estas etapas para solucionar o problema:  
  
1.  Verifique se o serviço de publicação World Wide Web está sendo executado primeiro navegando para o servidor https://usando o Internet Explorer. Se você não puder acessar o servidor Web dessa maneira, abra um prompt de comando e insira o comando a seguir, "NET START W3SVC".  
  
2.  No menu Iniciar, selecione executar. Digite msdfmap. ini e clique em OK para abrir o arquivo msdfmap. ini no bloco de notas. Marque a seção [conectar padrão] e, se o parâmetro de acesso estiver definido como NoAccess, altere-o para READONLY.  
  
3.  Usando o utilitário RegEdit, navegue até "HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\DataFactory\HandlerInfo" e certifique-se de que **HandlerRequired** está definido como 0 e **defaulthandler** é "" (cadeia de caracteres nula).  
  
     **Observação** Se você fizer alterações nessa seção do registro, deverá parar e reiniciar o serviço de publicação de World Wide Web inserindo os seguintes comandos em um prompt de comando: "NET STOP W3SVC" e "NET START W3SVC".  
  
4.  Usando o utilitário RegEdit, navegue no registro para "HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" e verifique se há uma chave chamada **RDSServer. datafactory**. Caso contrário, crie-o.  
  
5.  Usando Gerenciador de Serviços de Internet, localize o site da Web padrão e exiba as propriedades da raiz virtual do MSADC. Inspecione as restrições de segurança de diretório/endereço IP e nome de domínio. Se a opção "acesso negado" for marcada, selecione "concedido".  
  
 Certifique-se de tentar reinicializar o servidor se as alterações não aparecerem para resolver o problema primeiro.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565). A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows. Migre aplicativos que usam o RDS para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


