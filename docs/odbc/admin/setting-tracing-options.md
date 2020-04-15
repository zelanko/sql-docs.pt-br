---
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
ms.openlocfilehash: 21bee5d903459423a134389e62db844f5f63c9c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307187"
---
# <a name="setting-tracing-options"></a>Configurar opções de rastreamento
A guia **Rastreamento** da caixa de diálogo Administrador de origem de **dados ODBC** permite configurar a forma como as chamadas de função ODBC são rastreadas.  
  
## <a name="how-tracing-works"></a>Como funciona o rastreamento  
 Quando você começar a rastrear a partir da guia **Rastreamento,** o Gerenciador de driver registrará todas as chamadas de função ODBC para todos os aplicativos executados posteriormente. As chamadas de função ODBC de aplicativos que estão sendo executados antes do rastreamento ser iniciado não são registradas. As chamadas de função ODBC são gravadas em um arquivo de registro que você especificar.  
  
 O rastreamento só pára depois de clicar em **Parar de rastrear agora**. Lembre-se que enquanto o rastreamento estiver ligado, o arquivo de log continua a aumentar e que isso afeta o desempenho de todos os seus aplicativos ODBC.  
  
 Para obter mais informações sobre rastreamento, consulte [Tracing](../../odbc/reference/develop-app/tracing.md).  
  
### <a name="changes-in-odbc-tracing"></a>Mudanças no rastreamento do ODBC  
 Antes do MDAC 2.7 SP2, o rastreamento odbc só era permitido ocorrer em uma base de toda a máquina, na qual o rastreamento captura detalhes expostos sobre todos os aplicativos ODBC executados sob quaisquer identidades. Isso incluiu o rastreamento de atividades relacionadas ao ODBC que podem ocorrer para processos criados ou executados em nome de outras contas de usuários locais e princípios de segurança incorporados, como o Serviço Local e o Serviço de Rede.  
  
 Por padrão, o rastreamento ODBC agora usa o modo por usuário. Se você é um administrador local, no entanto, você ainda pode habilitar o rastreamento em toda a máquina usando o Administrador de Origem de Dados ODBC.  
  
 Para configurar o modo de rastreamento ODBC:  
  
1.  Se for necessário, faça login usando uma conta que tenha adesão ao grupo administradores locais.  
  
2.  A partir de Ferramentas Administrativas, abra o Administrador de Origem de Dados ODBC.  
  
3.  Clique na guia **Rastreamento.**  
  
4.  Configure o modo de rastreamento usando a **caixa de seleção de todas as identidades do usuário:**  
  
5.  Para habilitar o rastreamento em toda a máquina, selecione a caixa de seleção.  
  
6.  Para retornar ao rastreamento por usuário, limpe a caixa de seleção.  
  
7.  Clique em **Aplicar**.  
  
> [!NOTE]  
>  Se você já começou a rastrear em um modo, você tem que parar de rastrear e mudar para o outro modo para que o modo seja alterado com sucesso.  
  
> [!IMPORTANT]  
>  O rastreamento em toda a máquina só deve ser ativado quando necessário; caso contrário, ele deve ser deixado desligado.  
  
## <a name="visual-studio-analyzer-tracing"></a>Rastreamento do analisador do estúdio visual  
  
> [!IMPORTANT]  
>  O suporte para Visual Studio Analyzer foi removido a partir do Windows 8 (visual Studio Analyzer foi incluído apenas em versões mais antigas do Visual Studio.). Para um mecanismo alternativo de solução de problemas, use o rastreamento BID.  
  
 O Visual Studio® Analyzer Tracing fornece informações de desempenho e depuração sobre a camada ODBC. Todos os eventos de saída serão disparados na interface de alto nível para apresentar uma imagem o mais precisa possível em relação ao tempo gasto em componentes ODBC. Visual Studio Analyzer Tracing requer que qualquer fonte de evento se registre quando a fonte estiver configurada. Para obter mais informações sobre esse tipo de rastreamento, consulte a documentação do Visual Studio.
