---
title: "Definindo opções de rastreamento | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: admin
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual Studio Analyzer tracing [ODBC]
- ODBC data source administrator [ODBC], tracing options
- tracing options [ODBC], ODBC data source administrator
ms.assetid: 44404a79-b716-4bc1-9ffb-70cd8239d237
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b11d6337c2e0ca2853838d964842be536454c5f4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="setting-tracing-options"></a>Definindo opções de rastreamento
O **rastreamento** guia o **administrador de fonte de dados ODBC** caixa de diálogo permite que você configure a maneira como as chamadas de função ODBC são rastreadas.  
  
## <a name="how-tracing-works"></a>Como funciona o rastreamento  
 Quando você inicia o rastreamento do **rastreamento** guia, o Gerenciador de Driver registrará todas as chamadas de função ODBC para todos os posteriormente, executar aplicativos. Chamadas de função ODBC de aplicativos são executados antes do início do rastreamento não são registradas. Chamadas de função ODBC são registradas em um arquivo de log que você especificar.  
  
 Rastreamento será interrompido depois de clicar em **Parar rastreamento agora**. Lembre-se de que, enquanto o rastreamento está ativado, o arquivo de log continua a aumentar e que isso afetará o desempenho de todos os seus aplicativos de ODBC.  
  
 Para obter mais informações sobre rastreamento, consulte [rastreamento](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Alterações no rastreamento ODBC  
 Antes do MDAC 2.7 SP2, o rastreamento ODBC foi só pode ocorrer em uma base de todo o computador, no qual o rastreamento captura expostos detalhes sobre todos os aplicativos ODBC em execução em todas as identidades. Isso está incluído no rastreamento para a atividade de ODBC que pode ocorrer em processos criados ou executados em nome de outras contas de usuário local e entidades de segurança internas, como o serviço Local e serviço de rede.  
  
 Por padrão, o ODBC rastreamento agora usa o modo por usuário. Se você for um administrador local, no entanto, você pode ainda habilitar rastreamento de máquina usando o administrador de fonte de dados ODBC.  
  
 Para configurar o modo de rastreamento de ODBC:  
  
1.  Se for necessário, faça logon usando uma conta que tenha associação no grupo de administradores locais.  
  
2.  Em Ferramentas administrativas, abra o administrador de fonte de dados ODBC.  
  
3.  Clique o **rastreamento** guia.  
  
4.  Configurar o modo de rastreamento usando o **rastreamento de máquina para todas as identidades de usuário** caixa de seleção:  
  
5.  Para habilitar o rastreamento de máquina, marque a caixa de seleção.  
  
6.  Para retornar para o rastreamento por usuário, desmarque a caixa de seleção.  
  
7.  Clique em **Aplicar**.  
  
> [!NOTE]  
>  Se você já tiver iniciado o rastreamento em um modo, você precisa interromper o rastreamento e alternar para outro modo para o modo a ser alterada com êxito.  
  
> [!IMPORTANT]  
>  Rastreamento de todo o computador deve ser habilitado apenas quando for necessário; Caso contrário, ele deve ser deixado desativado.  
  
## <a name="visual-studio-analyzer-tracing"></a>Rastreamento do Visual Studio Analyzer  
  
> [!IMPORTANT]  
>  Suporte para Visual Studio Analyzer foi removido a partir do Windows 8 (Visual Studio Analyzer foi incluído somente nas versões anteriores do Visual Studio.). Para obter uma alternativa mecanismo de solução de problemas, use o rastreamento BID.  
  
 Rastreamento do Visual Studio® Analyzer fornece desempenho e informações de depuração sobre a camada de ODBC. Todos os eventos de saída serão disparados na interface de nível superior para apresentar uma imagem como precisas possível sobre tempo gasto em componentes ODBC. Rastreamento do Visual Studio Analyzer requer qualquer fonte de eventos para registrar quando a fonte é configurada. Para obter mais informações sobre esse tipo de rastreamento, consulte a documentação do Visual Studio.

