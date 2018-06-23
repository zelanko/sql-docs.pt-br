---
title: Ferramentas externas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.externaltools
helpviewer_keywords:
- External Tools dialog box
ms.assetid: d7dae88f-0781-4162-96cd-d3a3a4d82035
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ecaf04f54600f26489aa1b34ee1cbf69645752d0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115147"
---
# <a name="external-tools"></a>Ferramentas Externas
  Use esta caixa de diálogo para adicionar ferramentas externas, como o Gerenciador de Configurações do SQL Server ou o Bloco de Notas, ao menu **Ferramentas** . Adicionar ferramentas externas permite a execução de outros aplicativos facilmente enquanto você trabalha no ambiente do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você pode especificar argumentos e um diretório de trabalho na execução da ferramenta. Além disso, as saídas de algumas ferramentas podem ser exibidas na janela Saída. A caixa de diálogo **Ferramentas Externas** está disponível no menu **Ferramentas** .  
  
## <a name="options"></a>Opções  
 **Conteúdo do Menu**  
 Relaciona os títulos dos itens atuais adicionados ao menu **Ferramentas** . Use as setas **Mover para Cima** e **Mover para Baixo** para alterar a ordem dos itens que aparecem no menu. Use o botão **Excluir** para remover um item do menu.  
  
 **Mover para Cima**  
 Mova a ferramenta selecionada para cima na lista de ferramentas exibida no menu **Ferramentas** .  
  
 **Mover para Baixo**  
 Mova a ferramenta selecionada para baixo na lista de ferramentas exibida no menu **Ferramentas** .  
  
 **Adicionar**  
 Desmarque as caixas de texto para que você possa especificar uma nova ferramenta.  
  
 **Delete (excluir)**  
 Remova a ferramenta ou o comando da lista **Conteúdo do Menu** , bem como do menu **Ferramentas** .  
  
 **Título**  
 Nome da ferramenta ou do comando que será exibido no submenu **Ferramentas Externas** do menu **Ferramentas** . Coloque um E comercial (&amp;) antes de uma letra no nome da ferramenta para usar essa letra como uma tecla de atalho. Por exemplo, `&Spy++` exibiria **Spy++** no menu **Ferramentas** .  
  
 **Comando**  
 Especifique o caminho do .exe, .com, .pif, .bat, .cmd ou outro arquivo que você pretende abrir. A saída do `.bat`, `.com`e de outros arquivos pode ser exibida na janela Saída se você marcar a caixa de seleção **Usar janela Saída** .  
  
 **Argumentos**  
 Especifique as variáveis que serão passadas à ferramenta quando a ferramenta for selecionada no menu. Os argumentos podem especificar valores que são passados à ferramenta ou ao comando quando são iniciados. Por exemplo, um valor pode especificar um nome de arquivo ou diretório. Use o botão de **Seta** para fazer a seleção em uma lista de argumentos predefinidos. Você pode adicionar mais de um argumento. Para obter uma lista completa de argumentos predefinidos e suas definições, consulte [Arguments for External Tools](external-tools.md). Você também pode inserir argumentos personalizados (por exemplo, opções de prompt de comando), dependendo do comando ou da ferramenta usada.  
  
 **Diretório inicial**  
 Especifique o diretório de trabalho da ferramenta. Use o botão de **Seta** para selecionar diretórios. Você pode selecionar mais de um argumento.  
  
 **Use output Window**  
 Especifique se os resultados da ferramenta são ou não exibidos na janela Saída. Essa opção só se encontra disponível para arquivos, como .bat e .com, que normalmente exibem a saída na janela do prompt de comando. Quando habilitada, essa opção facilita o gerenciamento de janelas quando você segue o progresso de uma ferramenta.  
  
 **Solicitar argumentos**  
 Exiba a caixa de diálogo **Argumentos** para permitir a inserção ou edição de valores dos argumentos sempre que você iniciar a ferramenta externa.  
  
 **Tratar saída como Unicode**  
 Permita que a janela Saída aceite o Unicode.  
  
 **Fechar ao Sair**  
 Fecha a janela aberta pela ferramenta quando ela for encerrada.  
  
## <a name="example"></a>Exemplo  
  
#### <a name="to-add-sql-server-configuration-manager-to-the-tools-menu"></a>Para adicionar o Gerenciador de Configurações do SQL Server ao menu Ferramentas  
  
1.  No menu **Ferramentas** , clique em **Ferramentas Externas**.  
  
2.  Na caixa **Título** , digite **Gerenciador de Configurações do SQL Server**.  
  
3.  No **comando** , digite o caminho para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] executável, como Console de gerenciamento `C:\WINNT\system32\mmc.exe`  
  
4.  No **argumentos** , digite o caminho para o arquivo. msc, como `"C:\WINNT\system32\SQLServerManager.msc"`  
  
> [!NOTE]  
>  Veja as propriedades do atalho do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no menu **Iniciar** para confirmar o local dos arquivos em seu computador.  
  
  