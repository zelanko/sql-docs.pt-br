---
title: Alterações significativas para o Analysis Services Features in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 46
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a00010f10148d4ed949a7d5602a68fb6a53b3f6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238046"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>Alterações recentes em recursos do Analysis Services no SQL Server 2014
  Este tópico descreve as alterações recentes no [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]. Essas alterações podem interromper aplicativos, scripts ou funcionalidades baseados em versões anteriores do SQL Server.  
  
 Neste tópico:  
  
-   [Alterações recentes no SQL Server 2014](#bkmk_sql2014)  
  
-   [Alterações recentes no SQL Server 2012 SP1](#bkmk_2012Sp1)  
  
-   [Alterações recentes no SQL Server 2012](#bkmk_sql11)  
  
-   [Alterações recentes no SQL Server 2008/SQL Server 2008 R2](#bkmk_sql10)  
  
##  <a name="bkmk_sql2014"></a> Últimas alterações do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Há nenhum novo alteração significativa anunciada para mineração de dados tabular, multidimensional ou [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] recursos nesta versão.  No entanto, porque [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] é tão semelhante para o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] versões, alterações de ambas as versões anteriores são fornecidas aqui como uma conveniência, se você estiver atualizando do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="bkmk_2012Sp1"></a> Alterações recentes no SQL Server 2012 SP1  
 Alterações de código relacionadas à globalização comprovadamente interrompem alguns aplicativos. Os problemas conhecidos incluem:  
  
 **Diferenciação de maiusculas e minúsculas de identificadores de objeto**  
 Uma alteração de código destinada a fazer com que todos os identificadores de objeto não diferenciem maiúsculas e minúsculas está causando o efeito oposto em alguns idiomas. A intenção é que todos os identificadores de objeto não diferenciem maiúsculas de minúsculas, independentemente do agrupamento. Essa alteração alinha o Analysis Services com outros aplicativos geralmente usados na mesma pilha de solução.  
  
 Para idiomas com base em 26 caracteres do alfabeto latino básico, identificadores de objeto agora não diferenciam maiúsculas de minúsculas, que é o comportamento desejado.  
  
 Para cirílico e outros scripts de idioma bicamerais que usam maiúsculas/minúsculas (em grego, armênio, e copta), identificadores de objetos agora diferenciam maiúsculas de minúsculas. As alterações mais recentes têm mais probabilidade de ocorrer quando há diferenciação de maiúsculas/minúsculas entre um identificador de objeto e como ele é referenciado (por exemplo, um script de processamento que se refere ao identificador de objeto com todas as letras minúsculas). Esse comportamento provavelmente será alterado no futuro, mas como uma solução temporária é recomendável modificar os scripts para usar a mesma caixa que o identificador de objeto.  
  
##  <a name="bkmk_sql11"></a> Últimas alterações do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 Esta seção documenta as últimas alterações relatadas referentes [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] os recursos do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Problema|Description|  
|-----------|-----------------|  
|Comandos de instalação removidos para uma instalação do [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)].|A instalação é realizada, mas não configura mais um [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]. Os comandos de instalação que coletavam valores usados em ações de configuração agora são removidos. Eles incluem /FARMACCOUNT, /FARMPASSWORD, /PASSPHRASE e /FARMADMINPORT.<br /><br /> Se você criou scripts de instalação para instalação autônoma, precisará modificar esses scripts para uma instalação do [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]. A alternativa é usar cmdlets do PowerShell para configurar o servidor em modo autônomo. Para obter mais informações, consulte [instalar o PowerPivot do Prompt de comando](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md) e [configuração do PowerPivot usando o Windows PowerShell](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).|  
  
##  <a name="bkmk_sql10"></a> Alterações recentes no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 Esta seção contém as alterações de quebra de versões anteriores. Se você estiver atualizando do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], deverá revisar as alterações de quebra introduzidas no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
|Problema|Description|  
|-----------|-----------------|  
|A função shallow exists agora funciona de maneira diferente com conjuntos nomeados que contêm membros enumerados ou junções cruzadas de enumsets.|No [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], a função shallow exists não funcionava com conjuntos nomeados que continham membros enumerados ou interjunções de conjuntos de enumsets. Para compatibilidade com versões anteriores com o original versão versão e o SP1 do [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], defina a propriedade de configuração "ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode" como 1, ou para compatibilidade com versões anteriores [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] SP2, defina-o como 2.|  
|As funções do VBA lidam com valores nulos e vazios Diferentemente de como faziam no [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]|No [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], funções do VBA retornavam 0 ou uma cadeia vazia quando valores nulos ou vazios eram usados como argumentos. No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], elas retornarão nulo.|  
|O Assistente de Migração falhará porque o DSO não é instalado por padrão.|Por padrão, o SQL Server 2008 não instala o componente de compatibilidade com versões anteriores DSO (Decision Support Objects). O pacote de compatibilidade com versões anteriores é instalado por padrão, mas o componente DSO do pacote ficará desabilitado. Uma vez que o Assistente de Migração do SQL Server Analysis Services depende desse componente, ele falhará, a menos que o componente seja instalado. Para instalar o componente DSO, execute o seguinte procedimento:<br /><br /> 1) abra o painel de controle.<br />2) no Windows XP ou Windows Server 2003, selecione **adicionar ou remover programas**. No Windows Vista e Windows Server 2008, selecione **Programas e Recursos**.<br />3) clique com botão direito **compatibilidade com versões anteriores do Microsoft SQL Server 2005**e selecione **alteração**.<br />4) no Assistente de configuração de compatibilidade com versões anteriores, clique em **próxima**.<br />5) na página de manutenção do programa, selecione **Modify**e, em seguida, clique em **próxima**.<br />6) na página seleção de recursos, se Decision Support Objects (DSO) não estiver disponível, clique na seta para baixo e selecione **este recurso será instalado no disco rígido local**. Clique em **Avançar**.<br />7) em pronto para modificar a página do programa, clique em **instalar**.<br />8) quando a instalação for concluída, clique em **concluir**.<br /><br /> <br /><br /> É possível remover o DSO após o término da migração seguindo as etapas anteriores, alterando a opção do DSO para “**Este recurso não estará disponível**.”<br /><br /> Se o pacote de compatibilidade com versões anteriores não estiver instalado, você poderá instalá-lo usando a mídia de distribuição do SQL Server 2008. Observe que existem versões específicas de cada arquitetura de destino (x86, x64, ia64). Essas versões podem ser encontradas nos seguintes locais:<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|Não é recomendável colocar o local da partição na pasta Dados.|O servidor gerencia a pasta Dados e cria ou elimina pastas à medida que objetos são criados, excluídos e alterados. Por isso, é totalmente desaconselhável especificar um local de armazenamento da partição na pasta Dados, principalmente nas subpastas de bancos de dados, cubos e dimensões. Embora o servidor permita fazer isso com Create ou Alter, ele exibirá um aviso. Quando você atualiza os bancos de dados do SQL Server 2005 Analysis Services para [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services que têm locais de armazenamento de partição na pasta de dados, ela funcionará. Restore ou Sync exigirão que você remova os locais de armazenamento da partição da pasta Dados.|  
|Você pode obter resultados inesperados de consultas que usam a palavra-chave MDX "EXISTING" no Servidor Analítico da ProClarity e no Microsoft Office PerformancePoint Server 2007.|O Servidor Analítico da ProClarity e o Microsoft Office PerformancePoint Server 2007 usam a palavra-chave EXISTING da linguagem MDX incorretamente em certos cenários. Devido a alterações feitas no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services, essas consultas podem retornar resultados inesperados.|  
  
## <a name="see-also"></a>Consulte também  
 [Compatibilidade com versões anteriores do Analysis Services](analysis-services-backward-compatibility.md)  
  
  
