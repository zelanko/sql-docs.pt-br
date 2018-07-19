---
title: Caixa de diálogo Adicionar referência de banco de dados | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql.data.tools.adddatabasereference.dialog
ms.assetid: 838caa2a-4117-48bc-8c6c-9e7ceab38893
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b6ff2ecf1f5846e7f0875d34220f688d2419950
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093657"
---
# <a name="add-database-reference-dialog-box"></a>Caixa de diálogo Adicionar Referência de Banco de Dados
Este tópico descreve os procedimentos que você pode executar na caixa de diálogo **Adicionar Referência de Banco de Dados**.  
  
As referências de banco de dados permitem que você:  
  
Acesse objetos em outros bancos de dados.  
Um projeto pode referenciar outro banco de dados em qualquer servidor usando a resolução de nomes de três ou quatro partes. Ao usar um nome de três ou quatro partes para uma referência, você pode usar variáveis SQLCMD para permitir que as referências funcionem em vários servidores e bancos de dados.  
  
Crie uma solução composta de vários projetos de banco de dados.  
Em um projeto composto, as referências de banco de dados particionam um banco de dados grande em vários projetos separados. Você cria uma referência que não contém variáveis ou valores para o banco de dados ou servidor (usando apenas nomes de uma e duas partes).  
  
As referências de bancos de dados podem ser feitas para um projeto de banco de dados na solução atual ou para um DACPAC. A adição de uma referência de banco de dados a um projeto altera as dependências do projeto e a ordem de compilação.  
  
## <a name="selecting-the-database-to-reference"></a>Selecionando o banco de dados para referência  
Você pode referenciar outro projeto de banco de dados na mesma solução, um banco de dados do sistema ou um DACPAC.  
  
Se houver mais de um projeto de banco de dados em sua solução, a opção **Projetos de banco de dados na solução atual** será habilitada. Você pode referenciar outro banco de dados na solução.  
  
Selecione **Banco de dados do sistema** se você pretende selecionar um dos bancos de dados do sistema como uma referência de banco de dados.  
  
Selecione **Aplicativo da Camada de Dados (.dacpac)** para referenciar um banco de dados em um DACPAC, e procure o diretório com o arquivo DACPAC.  
  
## <a name="selecting-the-databases-relative-location"></a>Selecionando o local relativo do banco de dados  
Depois de selecionar o banco de dados que deseja referenciar, você pode especificar o local esperado de um objeto de banco de dados, relativo ao projeto de referência.  
  
As referências podem ser resolvidas para objetos em um dos seguintes locais:  
  
- No banco de dados de referência.  
  
- E um banco de dados diferente do banco de dados de referência, mas no mesmo servidor.  
  
- Em um banco de dados diferente do banco de dados de referência, em um servidor diferente.  
  
Especifique um nome de banco de dados. Se você escolher a opção **Banco de dados do sistema**, não será necessário modificar a literal do banco de dados do sistema. Se você escolher **Projetos de banco de dados na solução atual**, o nome padrão do banco de dados terá como base o nome do banco de dados no projeto.  
  
Se você selecionou **Banco de dados diferente, servidor diferente**, especifique um nome de servidor.  
  
Você pode usar uma variável de banco de dados (SQLCMD). Se desejar fazer referência ao banco de dados com uma variável (em vez do nome literal), aceite ou modifique a variável de banco de dados padrão. Uma variável de banco de dados será útil se você publicar o projeto de banco de dados de vários servidores e bancos de dados. Nesse caso, um desenvolvedor pode ir para **Variáveis SQLCMD** nas páginas de propriedades do projeto e especificar o nome local do banco de dados. Se você deixar **Variável de banco de dados** em branco, só poderá fazer referência ao banco de dados pelo seu nome literal. Se você especificar um nome de variável de banco de dados, não poderá fazer referência ao banco de dados pelo seu nome literal.  
  
Se você selecionou a opção **Banco de dados diferente, servidor diferente** uma variável de servidor (SQLCMD) será necessária. Uma variável de servidor será útil à publicação do projeto de banco de dados de vários servidores e bancos de dados. Nesse caso, um desenvolvedor pode ir para **Variáveis SQLCMD** nas páginas de propriedades do projeto e especificar o nome local do servidor. Você pode fazer referência ao servidor pelo nome da variável, e não pelo nome do servidor.  
  
> [!IMPORTANT]  
> Em algumas situações, você pode criar uma referência de banco de dados que tenha o mesmo nome que a referência de banco de dados existente. Duas referências de banco de dados com o mesmo nome podem resultar em comportamento inesperado. Nesse caso, exclua ambas as referências dos bancos de dados.  
  
## <a name="common-procedures"></a>Procedimentos comuns  
Veja a seguir os procedimentos comuns:  
  
### <a name="to-create-a-reference-to-a-database-on-the-same-server"></a>Para criar uma referência a um banco de dados no mesmo servidor  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** e selecione **Adicionar Referência de Banco de Dados**.  
  
2.  Na caixa de diálogo **Adicionar Referência de Banco de Dados**, especifique o **Local do Banco de Dados** como **Outro banco de dados, mesmo servidor**.  
  
3.  Especifique o nome do banco de dados.  
  
4.  Decida se você quer usar uma variável de banco de dados.  
  
5.  Copie o uso de exemplo e cole-o em seu arquivo .sql. No uso de exemplo, altere [Schema1] para o nome do esquema (por exemplo, [dbo]). Além disso, modifique o nome do objeto do banco de dados de acordo com o seu projeto.  
  
6.  Compile a solução.  
  
### <a name="to-create-a-reference-to-a-database-on-another-server"></a>Para criar uma referência a um banco de dados em outro servidor  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** e selecione **Adicionar Referência de Banco de Dados**.  
  
2.  Na caixa de diálogo **Adicionar Referência de Banco de Dados**, especifique o **Local do Banco de Dados** como **Banco de dados diferente, servidor diferente**.  
  
3.  Verifique se o nome do banco de dados está correto.  
  
4.  Decida se você quer usar uma variável de banco de dados.  
  
5.  Especifique o nome do servidor e a variável de servidor.  
  
6.  Copie o uso de exemplo e cole-o em seu arquivo .sql. No uso de exemplo, altere [Schema1] para o nome do esquema (por exemplo, [dbo]). Além disso, modifique o nome do objeto do banco de dados de acordo com o seu projeto.  
  
7.  Compile a solução.  
  
### <a name="to-create-a-composite-project"></a>Para criar um projeto composto  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse em **Referências** e selecione **Adicionar Referência de Banco de Dados**.  
  
2.  Selecione a fonte do banco de dados a qual você está fazendo referência (um projeto na solução ou um DACPAC).  
  
3.  Na caixa de diálogo **Adicionar Referência de Banco de Dados**, especifique o **Local do Banco de Dados** como **Mesmo banco de dados**.  
  
4.  Copie o uso de exemplo e cole-o em seu arquivo .sql. No uso de exemplo, altere [Schema1] para o nome do esquema. Além disso, modifique o nome do objeto do banco de dados de acordo com o seu projeto.  
  
5.  Compile a solução.  
  
Ao publicar esse projeto, você pode implantar projetos compostos na mesma solução em um único destino:  
  
1.  Clique com o botão direito do mouse no nome do projeto, no **Gerenciador de Soluções**, e selecione **Publicar** para exibir a caixa de diálogo **Publicar Banco de Dados**.  
  
2.  Na caixa de diálogo **Publicar Banco de Dados**, clique em **Avançado**.  
  
3.  Na caixa de diálogo **Configurações de Publicação Avançadas**, verifique se a opção **Incluir objetos compostos** está selecionada na lista **Opções de Implantação Avançadas**.  
  
## <a name="see-also"></a>Consulte Também  
[Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md)  
  
