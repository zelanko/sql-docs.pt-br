---
title: "Executar etapas do Windows PowerShell no SQL Server Agent | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# Executar etapas do Windows PowerShell no SQL Server Agent
  Use o SQL Server Agent para executar scripts do SQL Server PowerShell nas horas agendadas.  
  
1.  **Antes de começar:**  [Limitações e restrições](#LimitationsRestrictions)  
  
2.  **Para executar o PowerShell no SQL Server Agent, usando:**  [Etapa de Trabalho do PowerShell](#PShellJob), [Etapa de Trabalho de Prompt de Comando](#CmdExecJob)  
  
## Antes de começar  
 Existem vários tipos de etapas de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Cada tipo está associado a um subsistema que implementa um ambiente específico, como um agente de replicação ou ambiente de prompt de comando. Você pode codificar os scripts do Windows PowerShell e usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para incluir os scripts em trabalhos que são executados em horários programados ou em resposta a eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Scripts do Windows PowerShell podem ser executados usando uma etapa de trabalho de prompt de comando ou uma etapa de trabalho do PowerShell.  
  
1.  Use uma etapa de trabalho do PowerShell para fazer com que o subsistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent execute o utilitário **sqlps**, que inicia o PowerShell e importa o módulo **sqlps**.  
  
2.  Use uma etapa de trabalho de prompt de comando para executar o PowerShell.exe e especifique um script que importa o módulo **sqlps** .  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
  
> [!CAUTION]  
>  Cada etapa de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executa o PowerShell com o módulo **sqlps** inicia um processo que consome aproximadamente 20 MB de memória. A execução de um grande número de etapas de trabalho concorrentes do Windows PowerShell pode afetar o desempenho de forma negativa.  
  
##  <a name="PShellJob"></a> Criar uma etapa de trabalho do PowerShell  
 **Para criar uma etapa de trabalho do PowerShell**  
  
1.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criando trabalhos](../../ssms/agent/create-jobs.md).  
  
2.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
3.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
4.  Na lista **Tipo** , clique em **PowerShell**.  
  
5.  Na lista **Executar como** , selecione a conta proxy com as credenciais que o trabalho usará.  
  
6.  Na caixa **Comando** , digite a sintaxe do script PowerShell que será executada para a etapa de trabalho. Como alternativa, clique em **Abrir** e selecione um arquivo que contenha a sintaxe de script.  
  
7.  Clique na página **Avançado** para definir as seguintes opções de etapa de trabalho: a ação a tomar em caso de êxito ou falha da etapa, quantas vezes o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve tentar executar a etapa e com que frequência.  
  
##  <a name="CmdExecJob"></a> Criar uma etapa de trabalho de prompt de comando  
 **Para criar uma etapa de trabalho CmdExec **  
  
1.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criando trabalhos](../../ssms/agent/create-jobs.md).  
  
2.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
3.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
4.  Na lista **Tipo**, escolha **Sistema operacional (CmdExec)**.  
  
5.  Na lista **Executar como** , selecione a conta proxy com as credenciais que o trabalho usará. Por padrão, etapas de trabalho CmdExec são executadas no contexto da conta do serviço do SQL Server Agent .  
  
6.  Na caixa **Código de saída do processo de um comando bem sucedido** , insira um valor de 0 a 999999.  
  
7.  Na caixa **Comando** , digite powershell.exe com parâmetros que especificam o script do PowerShell a ser executado.  
  
8.  Clique na página **Avançado** para definir opções para a etapa de trabalho, como a ação a tomar em caso de êxito ou falha da etapa, quantas vezes o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve tentar executar a etapa e o arquivo onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode gravar a saída da etapa. Somente membros da função de servidor fixa **sysadmin** podem gravar a saída de etapas de trabalho em um arquivo do sistema operacional.  
  
## Consulte também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  