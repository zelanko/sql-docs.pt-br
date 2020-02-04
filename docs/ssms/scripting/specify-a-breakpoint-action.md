---
title: Especificar uma ação de ponto de interrupção
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint action
- Transact-SQL debugger, breakpoint when hit action
ms.assetid: f97f0097-6f51-40c1-b2e0-294a93ce1e1b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d4bffc7742a9833d8715c9479e051cdd732d7596
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253648"
---
# <a name="specify-a-breakpoint-action"></a>Especificar uma ação de ponto de interrupção

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Uma ação de ponto de interrupção **Quando Atingido** especifica uma tarefa personalizada que o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] executa para um ponto de interrupção. Se a contagem de ocorrências especificada for atingida, e qualquer condição de ponto de interrupção especificada for atendida, o depurador executará a ação especificada para o ponto de interrupção.

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]
  
##  <a name="BKMK_ActionConsiderations"></a> Considerações sobre a ação

A ação padrão de um ponto de interrupção é interromper a execução quando a contagem de ocorrências e a condição de ponto de interrupção são atendidas. O principal uso de uma ação **Quando Atingido** no depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] é imprimir informações na janela **Saída** do depurador especificando uma mensagem de impressão.  
  
Uma mensagem de impressão é especificada na opção **Imprimir uma Mensagem** e como uma cadeia de caracteres de texto que inclui expressões que contêm informações do [!INCLUDE[tsql](../../includes/tsql-md.md)] que está sendo depurado. As expressões incluem:  
  
-   Uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] entre chaves ({}). As expressões podem incluir variáveis, parâmetros e funções internas do [!INCLUDE[tsql](../../includes/tsql-md.md)] . Os exemplos incluem {@MyVariable}, {@NameParameter}, {@@SPID} ou {SERVERPROPERTY('ProcessID')}.  
  
-   Uma das seguintes palavras-chave:  
  
    1.  $ADDRESS retorna o nome do procedimento armazenado ou a função definida pelo usuário onde o ponto de interrupção foi definido. Se o ponto de interrupção for definido na janela do editor, $ADDRESS retornará o nome do arquivo de script que está sendo editado. $ADDRESS e $FUNCTION retornam as mesmas informações no depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
    2.  $CALLER retorna o nome da unidade do código [!INCLUDE[tsql](../../includes/tsql-md.md)] que chamou um procedimento armazenado ou uma função. Se o ponto de interrupção estiver na janela do editor, $CALLER retornará \<Nenhum chamador disponível>. Se o ponto de interrupção estiver em um procedimento armazenado ou se a função definida pelo usuário foi chamada do código na janela do editor, $CALLER retornará o nome do arquivo que está sendo editado. Se o ponto de interrupção estiver em um procedimento armazenado ou a função definida pelo usuário tiver sido chamada de outro procedimento armazenado ou função, $CALLER retornará o nome do procedimento ou da função de chamada.  
  
    3.  $CALLSTACK retornará a pilha de chamada de funções na cadeia que chamou o procedimento armazenado ou a função definida pelo usuário atual. Se o ponto de interrupção estiver na janela do editor, $CALLSTACK retornará o nome do arquivo de script que está sendo editado.  
  
    4.  $FUNCTION retorna o nome do procedimento armazenado ou a função definida pelo usuário onde o ponto de interrupção foi definido. Se o ponto de interrupção for definido na janela do editor, $FUNCTION retornará o nome do arquivo de script que está sendo editado.  
  
    5.  $PID e $PNAME retornam a ID e o nome do processo do sistema operacional que executa a instância do Mecanismo de Banco de Dados onde o [!INCLUDE[tsql](../../includes/tsql-md.md)] está em execução. $PID retorna a mesma ID que SERVERPROPERTY('ProcessID'), exceto pelo fato de que $PID é um valor hexadecimal enquanto SERVERPROPERTY('ProcessID') é um valor decimal.  
  
    6.  $TID e $TNAME retornam a ID e o nome do thread do sistema operacional que está executando o lote do [!INCLUDE[tsql](../../includes/tsql-md.md)] . O thread é associado ao processo que executa a instância do Mecanismo de Banco de Dados. $TID retorna o mesmo valor que SELECT kpid FROM sys.sysprocesses, WHERE spid = @@SPID; porém, $TID é um valor hexadecimal, enquanto kpid é um valor decimal.  
  
-   Você também pode usar o caractere de barra invertida (\\) como um caractere de escape para permitir chaves e barras invertidas na mensagem: \\{, \\} e \\\\.  
  
#### <a name="to-specify-a-when-hit-action"></a>Para especificar uma ação Quando Atingido  
  
1.  Na janela do editor, clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Quando Atingido** no menu de atalho.  
  
     -ou-  
  
     Na janela **Pontos de Interrupção** , clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Quando Atingido** no menu de atalho.  
  
2.  Na caixa de diálogo **Quando o Ponto de Interrupção for Atingido** , selecione o comportamento desejado:  
  
    1.  Selecione **Imprimir uma Mensagem** para imprimir uma mensagem na janela Saída do depurador quando o ponto de interrupção for atingido.  
  
    2.  A opção **Executar uma Macro** não está disponível no depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] e está em cinza.  
  
    3.  Selecione **Continuar execução** se você não deseja que o ponto de interrupção pause a execução. Essa opção estará ativa apenas se você tiver selecionado a opção **Imprimir uma Mensagem** .  
  
3.  Clique em **OK** para implementar as alterações ou em **Cancelar** para sair sem aplicar as alterações.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar uma condição de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-condition.md)   
 [Especificar uma contagem de ocorrências](../../relational-databases/scripting/specify-a-hit-count.md)  
