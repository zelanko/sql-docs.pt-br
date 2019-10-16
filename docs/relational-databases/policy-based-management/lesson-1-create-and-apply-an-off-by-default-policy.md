---
title: 'Lição 1: Criar e aplicar uma política desativada por padrão | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: security
ms.prod_service: database-engine
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d31367db-b7db-44c4-8df2-f1240474cf78
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d79c212b1bc960f46e816ad6d99ee4ee24722eac
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251286"
---
# <a name="lesson-1-create-and-apply-an-off-by-default-policy"></a>Lição 1: Criar e aplicar uma política desativada por padrão
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Usando as políticas do Gerenciamento Baseado em Políticas, você pode administrar uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um ou mais objetos de instâncias, instâncias de servidor, bancos de dados ou objetos de bancos de dados. Como administrador de banco de dados, você deseja garantir que determinados servidores não tenham o Database Mail habilitado. Nesta lição, você criará uma condição e uma política que definirão essa opção de servidor. Você testará o servidor para ver se ele obedece a política. Então, você usará a política para reconfigurar o servidor para fins de conformidade.  

## <a name="prerequisites"></a>Prerequisites
Para concluir este tutorial, é necessário ter o SQL Server Management Studio e acesso a um servidor que está executando o SQL Server. 

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
  
## <a name="create-the-mail-off-condition"></a>Criar a condição de correio desativado

1.  Em Pesquisador de Objetos, expanda **Gerenciamento**, **Gerenciamento de Política**, **Facetas**, clique com o botão direito do mouse em **Configuração da Área da Superfície**e clique em **Nova Condição**.  

    ![nova condição](Media/lesson-1-create-and-apply-an-off-by-default-policy/new-surface-area-condition.png)
  
2.  Na caixa de diálogo **Criar Nova Condição** , na caixa **Nome** , digite **Correspondência Desativada**.   
    1. Na caixa **Faceta** , confirme se a faceta **Configuração da Área da Superfície** está selecionada.
    1. Na área **Expressão**, na caixa **Campo**, selecione **\@DatabaseMailEnabled**, na caixa **Operador**, selecione **=** e, em **Valor**, selecione **False**.  
    1. Na página **Descrição** , digite uma descrição da condição e clique em **OK** para criar a condição.  

    ![Condição de correio desativado](Media/lesson-1-create-and-apply-an-off-by-default-policy/mail-off-condition.png) 
  
## <a name="create-the-off-by-default-policy"></a>Criar a política desativada por padrão  
  
1.  Em Pesquisador de Objetos, clique com o botão direito do mouse em **Configuração da Área da Superfície**e clique em **Nova Política**.  
  
2.  Na caixa de diálogo **Criar Nova Política** , na caixa **Nome** , digite **Desativada por Padrão**. 
    1. Deixe a caixa de seleção **Habilitada** desmarcada. A caixa de seleção **Habilitada** se aplica às políticas automatizadas, e essa política será executada sob demanda.
    1. Na caixa de seleção **Verificar condição** , role a tela para baixo até a área **Configuração da Área da Superfície** e selecione **Correspondência Desativada** como condição de verificação.
    1. A caixa **Em relação aos destinos** ficará em branco porque esta é uma política com escopo no servidor. 
    1. Na caixa de seleção **Modo de Avaliação** , selecione **Sob demanda** como modo de avaliação.
    1. Na caixa de seleção **Restrição de servidor** , selecione **Nenhuma**.
    1. Na página **Descrição** , digite uma descrição para a política.  

    ![Política desativada por padrão](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy.png)
  
9. Na página de descrição, é possível fornecer um hiperlink para uma página da Web para suas políticas na área **Hiperlink de ajuda adicional**. Na caixa **Texto a ser exibido** , digite o texto que aparecerá no hiperlink.
    1. Na caixa **Endereço** , digite um hiperlink para uma página Ajuda, como a home page do departamento de TI de sua empresa.
    1. Para confirmar o endereço abrindo a página da Web, clique em **Testar Link**.
    1. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    ![Link da Web da política desativada por padrão](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy-web-link.png)


## <a name="configure-server-to-run-off-by-default-policy"></a>Configurar servidor para executar a política desativada por padrão 

1.  No Pesquisador de Objetos, clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aponte para **Políticas**e clique em **Avaliar**.  

    ![avaliar política](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-policy.png)
  
2.  Na caixa de diálogo **Avaliar Políticas** , você pode selecionar as políticas de outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de um arquivo. Nesta etapa, deixe **Fonte** definida para a sua instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
    1. Na seção **Políticas** , selecione a política **Desativada por Padrão** .
    1. Para ver se o servidor está em conformidade com a política, clique em **Avaliar**.
    1. Na área **Resultados** , você verá um círculo verde com uma marca de seleção se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver em conformidade com a política. Você verá um círculo vermelho com um X se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não obedecer a política. 

   ![avaliar política desativada por padrão](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-off-by-default-policy.png)

  
6.  Na área **Detalhes de Destino** , você verá informações adicionais na coluna **Mensagem** se ocorrer algum erro. Na coluna **Mensagem** , clique em **Exibir** para ver um relatório com os resultados da verificação de cada propriedade de faceta verificada. 

    ![Exibir resultados da avaliação da política](Media/lesson-1-create-and-apply-an-off-by-default-policy/view-results-of-policy-evaluation.png)
  
7.  A descrição da política é exibida na parte inferior da página, e a seção **Ajuda adicional** exibe o hiperlink configurado para a política. Clique no hiperlink da mensagem para abrir a página da Web que você especificou quando criou a política.   

1.  Feche o navegador e a caixa de diálogo **Exibição Detalhada dos Resultados** .  

1. Se o servidor não estiver em conformidade e você quiser desabilitar o Database Mail, clique em **Aplicar** na página **Resultados da Avaliação** .  
  
10. Feche as caixas de diálogo **Exibição Detalhada dos Resultados** e **Avaliar Políticas** .   

   
## <a name="next-lesson"></a>Próxima lição  
[Lição 2: Criar e aplicar uma política de nomeação de padrões](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
