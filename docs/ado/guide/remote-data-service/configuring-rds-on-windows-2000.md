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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6230fb7ffbaa1226bc65d391d988ad064617998
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922893"
---
# <a name="configuring-rds-on-windows-2000"></a>Configurar o RDS no Windows 2000
Se você tiver dificuldade para obtenção de RDS para funcionar corretamente após a atualização para o Windows 2000, siga estas etapas para solucionar o problema:  
  
1.  Certifique-se de que o serviço de publicação na World Wide Web está sendo executado primeiro, navegar para https:// server usando o Internet Explorer. Se você não pode acessar o servidor Web dessa maneira, abra um prompt de comando e digite o comando a seguir, "NET iniciar W3SVC".  
  
2.  No menu Iniciar, selecione Executar. Digite msdfmap.ini e, em seguida, clique em Okey para abrir o arquivo msdfmap.ini no bloco de notas. Verifique a seção [conectar padrão] e se o parâmetro de acesso é definido como NOACCESS, alterá-lo como somente leitura.  
  
3.  Usando o utilitário RegEdit, navegue até "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo" e certifique-se **HandlerRequired** é definido como 0 e **DefaultHandler** é "" (nulos a cadeia de caracteres).  
  
     **Observação** se você fizer alterações a esta seção do registro, você deve parar e reiniciar o serviço de publicação na World Wide Web, inserindo os comandos a seguir no prompt de comando: "NET STOP W3SVC" e "NET iniciar W3SVC".  
  
4.  Usando o utilitário RegEdit, navegue no registro para "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" e verifique se há uma chave chamada **RDSServer.Datafactory**. Caso contrário, crie-o.  
  
5.  Usando o Gerenciador de serviços de Internet, localize o site da Web padrão e exibir as propriedades da raiz virtual MSADC. Inspecione o diretório segurança/endereço IP e restrições de nome de domínio. Se o "acesso negado" estiver marcado, em seguida, selecione "Granted".  
  
 Certifique-se de reinicializar o servidor se as alterações não são exibidos resolver o problema primeiro.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565). Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows. Migrar aplicativos que usam o RDS para [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


