---
description: Botões de comando do catálogo de endereços
title: Botões de comando do catálogo de endereços | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
author: rothja
ms.author: jroth
ms.openlocfilehash: 0abdb36a7ff51bdf0b01e21957c10ca8b9f995e4
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88758606"
---
# <a name="address-book-command-buttons"></a>Botões de comando do catálogo de endereços
O aplicativo de catálogo de endereços inclui os seguintes botões de comando:  
  
-   Um botão **Localizar** para enviar uma consulta ao banco de dados.  
  
-   Um botão **limpar** para limpar as caixas de texto antes de iniciar uma nova pesquisa.  
  
-   Um botão **Atualizar perfil** para salvar alterações em um registro de funcionário.  
  
-   Um botão **cancelar alterações** para descartar as alterações.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="find-button"></a>Botão Localizar  
 Clicar no botão **Localizar** ativa o procedimento Sub Find_OnClick do VBScript, que compila e envia a consulta SQL. Clicar nesse botão popula a grade de dados.  
  
## <a name="building-the-sql-query"></a>Criando a consulta SQL  
 A primeira parte do procedimento Find_OnClick sub cria a consulta SQL, uma frase por vez, acrescentando cadeias de caracteres de texto a uma instrução SQL SELECT global. Ele começa definindo a variável `myQuery` como uma instrução SQL SELECT que solicita todas as linhas de dados da tabela de fonte de dados. Em seguida, o procedimento Sub examina cada uma das quatro caixas de entrada na página.  
  
 Como o programa usa a palavra `like` na criação de instruções SQL, as consultas são subcadeias de pesquisa em vez de correspondências exatas.  
  
 Por exemplo, se a caixa **sobrenome** contivesse a entrada "Berge" e a caixa de **título** contivesse a entrada "gerente do programa", a instrução SQL (valor de `myQuery` ) lerá:  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 Se a consulta foi bem-sucedida, todas as pessoas com um sobrenome que contém o texto "Berge" (como Berge e Bergeron) e com um título contendo as palavras "gerente de programa" (por exemplo, gerente de programa, tecnologias avançadas) são exibidas na grade de dados HTML.  
  
## <a name="preparing-and-sending-the-query"></a>Preparando e enviando a consulta  
 A última parte do procedimento Find_OnClick sub consiste em duas instruções. A primeira instrução atribui a propriedade [SQL](../../reference/rds-api/sql-property.md) do [RDS. Objeto DataControl](../../reference/rds-api/datacontrol-object-rds.md) igual à consulta SQL criada dinamicamente. A segunda instrução faz com que o **RDS. Objeto DataControl** ( `DC1` ) para consultar o banco de dados e exibir os novos resultados da consulta na grade.  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>Botão Atualizar perfil  
 Clicar no botão **Atualizar perfil** ativa o procedimento Sub Update_OnClick do VBScript, que executa o [RDS. ](../../reference/rds-api/datacontrol-object-rds.md) `DC1` Métodos [SubmitChanges](../../reference/rds-api/submitchanges-method-rds.md) e [Refresh](../../reference/rds-api/refresh-method-rds.md) do objeto DataControl.  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 Quando `DC1.SubmitChanges` o é executado, o serviço de dados remoto empacota todas as informações de atualização e as envia para o servidor via http. A atualização é tudo ou nada; se uma parte da atualização não for bem-sucedida, nenhuma das alterações será feita e uma mensagem de status será retornada. `DC1.Refresh` Não é necessário após **SubmitChanges** com o Remote Data Service, mas garante dados atualizados.  
  
## <a name="cancel-changes-button"></a>Botão cancelar alterações  
 Clicar em **cancelar alterações** ativa o procedimento Sub Cancel_OnClick do VBScript, que executa o [RDS. Objeto DataControl](../../reference/rds-api/datacontrol-object-rds.md) (método `DC1)` [CancelUpdate](../../reference/rds-api/cancelupdate-method-rds.md) .  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 Quando `DC1.CancelUpdate` é executado, ele descarta todas as edições feitas por um usuário em um registro de funcionário na grade de dados desde a última consulta ou atualização. Ele restaura os valores originais.  
  
## <a name="see-also"></a>Consulte Também  
 [Botões de navegação do catálogo de endereços](./address-book-navigation-buttons.md)   
 [Objeto DataControl (RDS)](../../reference/rds-api/datacontrol-object-rds.md)