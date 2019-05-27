---
title: Instalar o Analysis Services no modo de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bf1a8ee0d5dd3dde585a027fd08fd833fb40304
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079906"
---
# <a name="install-analysis-services-in-tabular-mode"></a>Instalar o Analysis Services em modo Tabular
  Se você estiver instalando o Analysis Services para usar os novos recursos de modelagem tabular, você deverá instalar o Analysis Services em um modo de servidor que dá suporte a esse tipo de modelo. O modo de servidor é Tabular, e é configurado durante a instalação.  
  
 Depois de instalar o servidor nesse modo, você poderá usá-lo para hospedar soluções que você cria no designer de modelo tabular. Um servidor de modo tabular é exigido se você desejar acesso de dados de modelo tabular pela rede.  
  
 Você pode especificar o modo Tabular no Assistente de Instalação ou em uma instalação de linha de comando. As seções a seguir descrevem cada tipo de abordagem.  
  
## <a name="installation-wizard"></a>Assistente de instalação  
 A lista a seguir mostra a você quais páginas no assistente de Instalação do SQL Server são usadas para instalar o Analysis Services em modo Tabular:  
  
1.  Selecione o **Analysis Services** na Árvore de Recursos na Instalação.  
  
     ![Árvore de recursos de instalação mostrando o Analysis Services](../../../sql-server/install/media/ssas-setupas.gif "árvore de recursos de instalação mostrando o Analysis Services")  
  
2.  Na página de Configuração do Analysis Services, selecione o **Modo de Tabela**.  
  
     ![Página de configuração com as opções de configuração do Analysis Services](../../../sql-server/install/media/ssas-setupasconfig.gif "página de configuração com as opções de configuração do Analysis Services")  
  
 O modo Tabular usa o índice columnstore xVelocity de memória otimizada (VertiPaq), que é o armazenamento padrão para modelos tabulares que você implanta no Analysis Services. Depois de implantar soluções de modelo tabular no servidor, você pode configurar seletivamente soluções tabulares para usar o armazenamento em disco DirectQuery como uma alternativa ao armazenamento associada à memória.  
  
## <a name="command-line-setup"></a>Instalação de Linha de Comando  
 A Instalação do SQL Server inclui um novo parâmetro (`ASSERVERMODE`) que especifica o modo do servidor. O exemplo a seguir ilustra a instalação de linha de comando que instala o Analysis Services no modo de servidor Tabular.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 `INSTANCENAME` deve ter menos de 17 caracteres.  
  
 Todos os valores de conta de espaço reservado devem ser substituídos por contas e senhas válidas.  
  
 Ferramentas como o SQL Server Management Studio ou [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] não são instaladas usando a sintaxe de linha de comando de exemplo que é fornecida. Para obter mais informações sobre como adicionar recursos, consulte [instalar o SQL Server 2014 do Prompt de comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 `ASSERVERMODE` diferencia maiúsculas e minúsculas.  Todos os valores devem ser expressos em maiúsculas. A tabela a seguir descreve os valores válidos para `ASSERVERMODE`.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|Este é o valor padrão. Se você não configurar o `ASSERVERMODE`, o servidor será instalado no modo de servidor Multidimensional.|  
|POWERPIVOT|Esse valor é opcional. Na prática, se você configura o parâmetro `ROLE`, o modo de servidor é automaticamente definido como 1, tornando `ASSERVERMODE` opcional para uma instalação do PowerPivot para SharePoint. Para obter mais informações, consulte [Install PowerPivot from the Command Prompt](../../../sql-server/install/install-powerpivot-from-the-command-prompt.md).|  
|TABULAR|Esse valor é obrigatório se você estiver instalando o Analysis Services no modo Tabular usando a instalação de linha de comando.|  
  
## <a name="see-also"></a>Consulte também  
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Configure o acesso do DirectQuery para um banco de dados do modelo de tabela ou na memória](../../tabular-models/enable-directquery-mode-in-ssms.md)   
 [Modelagem de tabela &#40;Tabular do SSAS&#41;](../../tabular-models/tabular-models-ssas.md)  
  
  
