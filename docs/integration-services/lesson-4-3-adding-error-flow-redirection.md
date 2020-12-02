---
description: 'Lição 4-3: Adicionar redirecionamento de fluxo de erro'
title: 'Etapa 3: Adicionar redirecionamento de fluxo de erro | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: daade3348f7384ed83365923bf94af7b211d6422
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88457119"
---
# <a name="lesson-4-3-add-error-flow-redirection"></a>Lição 4-3: Adicionar redirecionamento de fluxo de erro

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Na tarefa anterior, a transformação Pesquisar Chave de Moeda não pode gerar uma correspondência quando a transformação tenta processar o arquivo simples de amostra corrompido, o que produz um erro. Como a transformação usa as configurações padrão da saída de erro, qualquer erro faz a transformação falhar. Quando a transformação falha, o resto do pacote também falha.  
  
Em vez de permitir a falha da transformação, você pode configurar o componente para redirecionar a linha com falha para outro caminho de processamento usando a saída de erro. Usar um caminho de processamento de erros separado oferece mais opções. Por exemplo, você pode limpar os dados e depois reprocessar a linha com falha. Também é possível salvar a linha com falha junto com suas informações de erro para verificação e reprocessamento posteriores.  
  
Nesta tarefa, você configura a transformação Pesquisar Chave de Moeda para redirecionar linhas com falha para a saída de erro. No branch de erro do fluxo de dados, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] grava essas linhas em um arquivo.  
  
Por padrão as duas colunas extras em uma saída de erro do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], **ErrorCode** e **ErrorColumn**, só contêm um código de erro numérico e a ID da coluna na qual o erro ocorreu. Nesta tarefa, antes de o pacote gravar linhas com falha no arquivo, você usa um componente de Script para acessar a API [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e obter uma descrição do erro.  
  
## <a name="configure-an-error-output"></a>Configurar uma saída de erro  
  
1.  Na **Caixa de Ferramentas do SSIS**, expanda **Comum** e arraste o **Componente Script** para a superfície de design da guia **Fluxo de Dados** . Coloque **Script** à direita da transformação **Pesquisa de Códigos de Moeda** .  
  
2.  Na caixa de diálogo **Selecionar Tipo de Componente do Script**, selecione **Transformação** e selecione **OK**.  
  
3.  Para conectar os dois componentes, selecione a transformação **Pesquisar Chave de Moeda** e depois arraste a seta vermelha para a nova transformação **Script**.  
  
    A seta vermelha representa a saída de erro da transformação **Pesquisa de Códigos de Moeda** . Usando a seta vermelha para conectar a transformação ao componente Script, você redireciona qualquer erro de processamento ao componente Script, que processará os erros e os enviará ao destino.  
  
4.  Na caixa de diálogo **Configurar Saída de Erro**, na coluna **Erro**, selecione **Redirecionar linha** e, em seguida, selecione **OK**.  
  
5.  Na superfície de design **Fluxo de Dados**, selecione o nome **Componente Script** no novo **ScriptComponent** e altere o nome para **Obter Descrição do Erro**.  
  
6.  Clique duas vezes na transformação **Obter Descrição do Erro** .  
  
7.  Na caixa de diálogo **Editor de Transformação Scripts** , na página **Colunas de Entrada** , selecione a coluna **ErrorCode** .  
  
8.  Na página **Entradas e Saídas**, expanda **Saída 0**, selecione **Colunas de Saída** e selecione **Adicionar Coluna**.  
  
9. Na propriedade **Name**, insira *ErrorDescription* e defina a propriedade **DataType** como **Cadeia de caracteres Unicode [DT_WSTR]**.  
  
10. Na página **Script**, verifique se a propriedade **LocaleID** está definida como **Inglês (Estados Unidos)**.
  
11. Selecione **Editar Script** para abrir o  VSTA ([!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications). No método **Input0_ProcessInputRow**, insira ou cole o código a seguir:  
  
    [Visual Basic]  
  
    ```vb  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
    [Visual C#]  
  
    ```cs
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
    A sub-rotina concluída se parece com o código a seguir:  
  
    [Visual Basic]  
  
    ```vb
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
    [Visual C#]  
  
    ```cs
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. No menu **Compilar**, selecione **Compilar solução** para criar o script e salvar suas alterações, então feche o VSTA.  
  
13. Selecione **OK** para fechar a caixa de diálogo **Editor de Transformação Scripts**.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 4: Adicionar um destino de Arquivo Simples](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
  
  
