---
title: 'Etapa 2: Converter o projeto no Modelo de Implantação de Projeto | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 80964293-f1f5-4da7-b1fb-00ab8c30c1c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e03317e9d37387e6c2482aea3bdf102a0b063b03
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721188"
---
# <a name="lesson-6-2-convert-the-project-to-the-project-deployment-model"></a>Lição 6-2: Converter o projeto no Modelo de Implantação de Projeto

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nesta tarefa, você usa o Assistente de Conversão de Projeto do Integration Services para converter o projeto no Modelo de Implantação de Projeto.  
  
1.  No menu **Projeto**, selecione **Converter em Modelo de Implantação de Projeto**.  
  
2.  Na página **Introdução** do **Assistente de Conversão de Projeto do Integration Services**, examine as etapas e selecione **Avançar**.  
  
3.  Na página **Selecionar Pacotes**, na lista **Pacotes**, desmarque todas as caixas de seleção, exceto **Lesson 6.dtsx** e selecione **Avançar**.  
  
4.  Na página **Especificar Propriedades do Projeto**, selecione **Avançar**.  
  
5.  Na página **Atualizar Tarefa de Execução do Pacote**, selecione **Avançar**.  
  
6.  Na página **Selecionar Configurações**, verifique se o pacote da **Lesson 6.dtsx** está selecionado na lista **Configurações** e selecione **Avançar**.  
  
7.  Na página **Criar Parâmetros**, verifique se o pacote **Lesson 6.dtsx** está selecionado.  Verifique se o **Escopo** é **Pacote** na lista **Propriedades de Configuração** e, em seguida, selecione **Avançar**.  
  
8.  Na página **Configurar Parâmetros**, verifique se os valores de **Nome** e **Valor** são os mesmos especificados na Lição 5 para a variável e o valor de configuração e selecione **Avançar**.  
  
9. Na página **Examinar**, no painel **Resumo**, observe que o assistente usou as informações do arquivo de configuração para definir as **Propriedades** a serem convertidas.  
  
10. Selecione **Converter**.  
  
    Depois que a conversão for concluída, você verá uma mensagem de aviso informando que as alterações não serão salvas até que você salve o projeto. Selecione **OK** para fechar a caixa de diálogo de aviso.  
  
11. No **Assistente de Conversão de Projeto do Integration Services**, selecione **Fechar**.  
  
12. Em **SQL Server Data Tools**, clique no menu **Arquivo** e selecione **Salvar** para salvar o pacote convertido.  
  
13. Selecione a guia **Parâmetros** e verifique se o pacote agora contém um parâmetro para **VarFolderName**. Esse valor de parâmetro é o mesmo caminho especificado para a pasta **Novos Dados de Exemplo** no arquivo de configuração da Lição 5.  
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 3: Testar o pacote da Lição 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
  
  
