---
title: Opções (página Editor de texto – Transact-SQL – geral) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.General
dev_langs:
- TSQL
ms.assetid: 7021ecb7-8fb5-4d8c-b984-3d34fcde8be2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f32377fffb26ac622dc4045d108e491adc2b0342
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089165"
---
# <a name="options-text-editor---transact-sql--general-page"></a>Opções (página Editor de texto – Transact-SQL – geral)
  Use a caixa de diálogo de opções **Geral** para alterar o comportamento de edição geral do Editor de Consultas do [!INCLUDE[ssDE](../includes/ssde-md.md)] , que é usado para editar scripts [!INCLUDE[tsql](../includes/tsql-md.md)] . Para exibir essas configurações, clique em **Opções** no menu **Ferramentas**, expanda a subpasta **Transact-SQL** e clique em **Geral**.  
  
## <a name="setting-options-in-multiple-locations"></a>Definindo as opções em vários locais  
 As opções para [!INCLUDE[ssDE](../includes/ssde-md.md)] o editor de consultas também podem ser definidas na caixa de diálogo **todos os idiomas geral** . Se você usar as caixas de diálogo **todos os idiomas** para definir opções diferentes para [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] os outros editores, como os editores DMX ou MDX, você deverá redefinir [!INCLUDE[ssDE](../includes/ssde-md.md)] as opções do editor de consultas usando essa caixa de diálogo.  
  
## <a name="statement-completion"></a>Conclusão de instrução  
 **Listar membros automaticamente**  
 Quando essa caixa de seleção estiver marcada, serão exibidos os bancos de dados e objetos de esquema, colunas, funções com valor de tabela ou funções à medida que forem digitados no editor. Escolha qualquer item na lista pop-up para inseri-lo em seu código.  
  
 **Ocultar membros avançados**  
 Esta caixa de seleção não está disponível.  
  
 **Informações de parâmetro**  
 Quando essa caixa de seleção está marcada, as informações de parâmetros são exibidas para um procedimento armazenado ou função que está imediatamente à esquerda do ponto de inserção (cursor). As informações incluem uma lista dos parâmetros disponíveis com os nomes e tipos de dados.  
  
## <a name="settings"></a>Configurações  
 **Habilitar espaço virtual**  
 Quando esta caixa de seleção está marcada, você pode clicar em qualquer ponto além do final de uma linha de código e digitar. Marque esta caixa de seleção para posicionar comentários em um ponto consistente próximo ao código. Marcar essa caixa de seleção desabilita a caixa de seleção **Quebra automática de linha** .  
  
 **Quebra automática de palavra**  
 Quando esta caixa de seleção estiver marcada, qualquer parte de uma linha que se estenda horizontalmente além da área do editor será automaticamente exibida na próxima linha. Marcar essa caixa de seleção habilita a caixa de seleção **Mostrar glifos visuais para quebra automática de linha** e desabilita a caixa de seleção **Habilitar espaço virtual** .  
  
 **Mostrar glifos visuais para quebra automática de linha**  
 Quando esta caixa de seleção está marcada, um indicador de seta de retorno é exibido no local em que uma linha longa é quebrada para a linha seguinte.  
  
 **Aplicar comandos Recortar/Copiar a linhas em branco quando não houver seleção**  
 Esta caixa de seleção define o comportamento do editor quando você coloca o ponto de inserção em uma linha em branco, não seleciona nada e clica em **Copiar** ou **Recortar**.  
  
 Quando essa caixa de seleção está marcada, a linha em branco é copiada ou recortada. Se você clicar em **Colar**, uma nova linha em branco será inserida.  
  
 Quando essa caixa de seleção é desmarcada, nada é copiado nem recortado. Se você clicar em **Colar**, o conteúdo mais recentemente copiado será colado. Se nada foi copiado anteriormente, nada será colado.  
  
 Essa configuração não tem nenhum efeito em **Copiar** ou **Recortar** quando uma linha não está em branco. Se nada for selecionado, a linha inteira será copiada ou recortada. Se você clicar em **Colar**, o texto da linha inteira e seu caractere de término serão colados.  
  
## <a name="display"></a>Exibição  
 **Números de linha**  
 Quando esta caixa de seleção estiver marcada, será exibido um número de linha ao lado de cada linha de código.  
  
> [!NOTE]  
>  Esses números de linha não são adicionados ao seu código e não aparecem na impressão. Eles são somente para referência.  
  
 **Habilitar navegação de URL com um só clique**  
 Quando esta caixa de seleção estiver marcada, o cursor mudará para um símbolo de mão de apontamento ao passar sobre uma URL no editor. Você pode clicar no URL para exibir a página indicada em seu navegador da Web.  
  
 **Barra de navegação**  
 Esta caixa de seleção não está disponível.  
  
  
