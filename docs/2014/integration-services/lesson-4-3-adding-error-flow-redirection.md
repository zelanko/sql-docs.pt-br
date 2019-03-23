---
title: 'Etapa 3: Adicionando redirecionamento de fluxo de erro | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dd2fd95b1ad2d239d055b2b49b991860a58d338
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58380444"
---
# <a name="step-3-adding-error-flow-redirection"></a>Etapa 3: Adicionando redirecionamento de fluxo de erro
  Conforme mostrado na tarefa anterior, a transformação Pesquisa de Códigos de Moeda não pode gerar uma correspondência quando a transformação tenta processar o arquivo simples de amostra corrompido que produziu um erro. Como a transformação usa as configurações padrão da saída de erro, qualquer erro faz a transformação falhar. Quando a transformação falha, o resto do pacote também falha.  
  
 Em vez de permitir a falha da transformação, você pode configurar o componente para redirecionar a linha com falha para outro caminho de processamento usando a saída de erro. O uso de um caminho de tratamento separado de erro permite que você faça várias coisas. Por exemplo, você pode tentar limpar os dados e depois reprocessar a linha com falha. Também é possível salvar a linha com falha junto com informações de erro adicionais para verificação e reprocessamento posteriores.  
  
 Nesta tarefa, você configurará a transformação Pesquisa de Códigos de Moeda para redirecionar linhas com falha para a saída de erro. Na ramificação de erro do fluxo de dados, essas filas serão gravadas em um arquivo.  
  
 Por padrão as duas colunas extras em uma saída de erro do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , **ErrorCode** e **ErrorColumn**, só contêm códigos numéricos que representam um número de erro e a ID da coluna na qual o erro aconteceu. Esses valores numéricos podem ter uso limitado sem a descrição de erro correspondente.  
  
 Para aumentar a utilidade da saída de erro, antes de o pacote gravar as linhas com falha no arquivo, você usará um componente Script para acessar a API do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e obter uma descrição do erro.  
  
### <a name="to-configure-an-error-output"></a>Para configurar uma saída de erro  
  
1.  Na **Caixa de Ferramentas do SSIS**, expanda **Comum**e arraste o **Componente Script** para a superfície de design da guia **Fluxo de Dados** . Coloque **Script** à direita da transformação **Pesquisa de Códigos de Moeda** .  
  
2.  Na caixa de diálogo **Selecionar Tipo de Componente do Script** , clique em **Transformação**e clique em **OK**.  
  
3.  Clique na transformação **Pesquisa de Códigos de Moeda** e depois arraste a seta vermelha sobre a transformação **Scripts** adicionada recentemente para conectar os dois componentes.  
  
     A seta vermelha representa a saída de erro da transformação **Pesquisa de Códigos de Moeda** . Usando a seta vermelha para conectar a transformação ao componente Script, você pode redirecionar qualquer erro de processamento ao componente Script, que então processará os erros e os enviará ao destino.  
  
4.  Na caixa de diálogo **Configurar Saída de Erro** , na coluna **Erro** , selecione **Redirecionar linha**e, em seguida, clique em **OK**.  
  
5.  Na superfície de design **Fluxo de Dados** , clique em **Componente Script** , no **ScriptComponent**recém-adicionado e altere o nome para **Obter Descrição do Erro**.  
  
6.  Clique duas vezes na transformação **Obter Descrição do Erro** .  
  
7.  Na caixa de diálogo **Editor de Transformação Scripts** , na página **Colunas de Entrada** , selecione a coluna **ErrorCode** .  
  
8.  Na página **Entradas e Saídas** , expanda **Saída 0**, clique em **Colunas de Saída**e clique em **Adicionar Coluna**.  
  
9. No `Name` propriedade, digite **ErrorDescription** e defina o `DataType` propriedade a ser **cadeia de caracteres Unicode [DT_WSTR]**.  
  
10. Sobre o **Script** página, verifique o `LocaleID` estiver definida como **inglês (Estados Unidos.**  
  
11. Clique em **Editar Script** para abrir o VSTA ( [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications). No método `Input0_ProcessInputRow`, digite ou cole o código a seguir.  
  
     [Visual Basic]  
  
    ```  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
     [Visual C#]  
  
    ```  
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
     A sub-rotina concluída se parecerá com o código a seguir.  
  
     [Visual Basic]  
  
    ```  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
     [Visual C#]  
  
    ```  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. No menu **Compilar** , clique em **Compilar solução** para criar o script, salvar suas alterações e fechar o VSTA.  
  
13. Clique em **OK** para fechar a caixa de diálogo **Editor de Transformação Scripts** .  
  
## <a name="next-steps"></a>Próximas etapas  
 [Etapa 4: Adicionando um destino de arquivo simples] (lesson-4-4-adding-a-flat-file-destination.md  
  
  
