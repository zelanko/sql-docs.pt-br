---
description: Configurar opções de rastreamento
title: Definindo opções de rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72e3805eded00b1bfa0c984d5ff0ace1ae1494fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476948"
---
# <a name="setting-tracing-options"></a>Configurar opções de rastreamento
A guia **rastreamento** da caixa de diálogo **administrador de fonte de dados ODBC** permite que você configure a maneira como as chamadas de função ODBC são rastreadas.  
  
## <a name="how-tracing-works"></a>Como funciona o rastreamento  
 Quando você iniciar o rastreamento na guia **rastreamento** , o Gerenciador de driver registrará todas as chamadas de função ODBC para todos os aplicativos executados posteriormente. As chamadas de função ODBC de aplicativos que estão em execução antes de o rastreamento ser iniciado não são registradas. As chamadas de função ODBC são registradas em um arquivo de log que você especificar.  
  
 O rastreamento é interrompido somente depois que você clica em **parar rastreamento agora**. Lembre-se de que enquanto o rastreamento está ativado, o arquivo de log continua a aumentar e isso afeta o desempenho de todos os seus aplicativos ODBC.  
  
 Para obter mais informações sobre rastreamento, consulte [Tracing](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Alterações no rastreamento ODBC  
 Antes do MDAC 2,7 SP2, o rastreamento de ODBC só permitia ocorrer em toda a máquina, na qual o rastreamento captura detalhes expostos sobre todos os aplicativos ODBC em execução sob qualquer identidade. Isso inclui o rastreamento de atividades relacionadas a ODBC que podem ocorrer para processos criados ou executados em nome de outras contas de usuário local e entidades de segurança internas, como o serviço local e o serviço de rede.  
  
 Por padrão, o rastreamento ODBC agora usa o modo por usuário. No entanto, se você for um administrador local, ainda poderá habilitar o rastreamento em todo o computador usando o administrador de fonte de dados ODBC.  
  
 Para configurar o modo de rastreamento ODBC:  
  
1.  Se necessário, faça logon usando uma conta que tenha associação no grupo Administradores local.  
  
2.  Em ferramentas administrativas, abra o administrador de fonte de dados ODBC.  
  
3.  Clique na guia **Rastreamento**.  
  
4.  Configure o modo de rastreamento usando a caixa de seleção **rastreamento em todo o computador para todas as identidades de usuário** :  
  
5.  Para habilitar o rastreamento em todo o computador, marque a caixa de seleção.  
  
6.  Para retornar ao rastreamento por usuário, desmarque a caixa de seleção.  
  
7.  Clique em **Aplicar**.  
  
> [!NOTE]  
>  Se você já tiver iniciado o rastreamento em um modo, será necessário interromper o rastreamento e alternar para o outro modo para que o modo seja alterado com êxito.  
  
> [!IMPORTANT]  
>  O rastreamento em todo o computador só deve ser habilitado quando necessário; caso contrário, ela deve ser deixada desativada.  
  
## <a name="visual-studio-analyzer-tracing"></a>Rastreamento de Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  O suporte para Visual Studio Analyzer foi removido a partir do Windows 8 (Visual Studio Analyzer foi incluído apenas em versões anteriores do Visual Studio.). Para obter um mecanismo de solução de problemas alternativo, use o rastreamento de LICITAção.  
  
 O rastreamento do Visual Studio® Analyzer fornece informações de desempenho e depuração sobre a camada ODBC. Todos os eventos de saída serão acionados na interface de nível superior para apresentar o máximo possível de uma imagem com relação ao tempo gasto em componentes ODBC. O rastreamento de Visual Studio Analyzer exige que qualquer origem de evento seja registrada quando a fonte for configurada. Para obter mais informações sobre esse tipo de rastreamento, consulte a documentação do Visual Studio.
