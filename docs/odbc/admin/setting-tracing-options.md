---
title: Configurando opções de rastreamento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ccf5afd559d4d3716c22b42665c516aa230fafe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626574"
---
# <a name="setting-tracing-options"></a>Configurar opções de rastreamento
O **rastreamento** guia o **administrador de fonte de dados ODBC** caixa de diálogo lhe permite configurar o modo como as chamadas de função ODBC são rastreadas.  
  
## <a name="how-tracing-works"></a>Como funciona o rastreamento  
 Quando você inicia o rastreamento do **rastreamento** guia, o Gerenciador de Driver registrará em log todas as chamadas de função ODBC para todos, subsequentemente, executar aplicativos. Chamadas de função ODBC de aplicativos que são executados antes que o rastreamento seja iniciado não estão conectadas. Chamadas de função ODBC são registradas no arquivo de log que você especificar.  
  
 Rastreamento será interrompido depois de clicar em **Parar rastreamento agora**. Lembre-se de que, enquanto o rastreamento estiver ativada, o arquivo de log continua a aumentar e que isso afeta o desempenho de todos os seus aplicativos de ODBC.  
  
 Para obter mais informações sobre rastreamento, consulte [rastreamento](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Alterações no rastreamento ODBC  
 Antes do SP2 do MDAC 2.7, rastreamento ODBC foi só pode ocorrer em uma base de todo o computador, no qual o rastreamento captura expostos detalhes sobre todos os aplicativos ODBC em execução em todas as identidades. Isso incluiu o rastreamento para atividades relacionadas ao ODBC que podem ocorrer em processos criados ou executados em nome de outras contas de usuário local e entidades de segurança internas, como o serviço Local e o serviço de rede.  
  
 Por padrão, o ODBC rastreamento agora usa o modo por usuário. Se você for um administrador local, no entanto, você ainda poderá habilitar o rastreamento de todo o computador usando o administrador de fonte de dados ODBC.  
  
 Para configurar o modo de rastreamento de ODBC:  
  
1.  Se for necessário, faça logon usando uma conta que tenha associação no grupo de Administradores Local.  
  
2.  Em Ferramentas administrativas, abra o administrador de fonte de dados ODBC.  
  
3.  Clique o **rastreamento** guia.  
  
4.  Configurar o modo de rastreamento usando o **rastreamento de todo o computador para todas as identidades de usuário** caixa de seleção:  
  
5.  Para habilitar o rastreamento de todo o computador, selecione a caixa de seleção.  
  
6.  Para retornar para o rastreamento por usuário, desmarque a caixa de seleção.  
  
7.  Clique em **Aplicar**.  
  
> [!NOTE]  
>  Se você já tiver iniciado o rastreamento em um modo, você precisa interromper o rastreamento e alternar para outro modo para o modo a ser alterado com êxito.  
  
> [!IMPORTANT]  
>  Rastreamento de todo o computador deve ser habilitado apenas quando for necessário; Caso contrário, ele deverá ser deixado desativado.  
  
## <a name="visual-studio-analyzer-tracing"></a>Rastreamento do Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  Suporte para o analisador do Visual Studio foi removido a partir do Windows 8 (Visual Studio Analyzer foi incluído apenas em versões mais antigas do Visual Studio.). Para obter uma alternativa de mecanismo de solução de problemas, use o rastreamento da oferta.  
  
 Rastreamento do Visual Studio® Analyzer fornece desempenho e informações de depuração sobre a camada ODBC. Todos os eventos de saída serão disparados na interface de nível superior para apresentar uma imagem como precisas quanto possível sobre tempo gasto em componentes de ODBC. Rastreamento do Visual Studio Analyzer exige a qualquer fonte de eventos para registrar quando a fonte é configurada. Para obter mais informações sobre esse tipo de rastreamento, consulte a documentação do Visual Studio.
