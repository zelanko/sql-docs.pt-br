---
title: "Botões de comando do catálogo de endereços | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO], command buttons
- RDS scenarios [ADO], command buttons
ms.assetid: 80676831-6488-4dad-a558-c47c52256a22
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1618d681f19e3aff5885a61f347ebbb7481bd1ff
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="address-book-command-buttons"></a>Botões de comando do catálogo de endereços
O aplicativo de catálogo de endereços inclui os seguintes botões de comando:  
  
-   Um **localizar** botão para enviar uma consulta ao banco de dados.  
  
-   Um **limpar** botão desmarcar as caixas de texto antes de iniciar uma nova pesquisa.  
  
-   Um **atualizar perfil** botão para salvar as alterações em um registro de funcionário.  
  
-   Um **Cancelar alterações** botão para descartar as alterações.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="find-button"></a>Botão Localizar  
 Clique o **localizar** botão ativa o procedimento de VBScript Find_OnClick Sub, que cria e envia a consulta SQL. Este botão preenche a grade de dados.  
  
## <a name="building-the-sql-query"></a>Criar a consulta SQL  
 A primeira parte do procedimento Sub Find_OnClick cria a consulta SQL, uma só vez, acrescentando cadeias de caracteres de texto para uma instrução de SQL SELECT global. Ele começa definindo a variável `myQuery` para uma instrução SQL SELECT que solicita a todas as linhas de dados da tabela de fonte de dados. Em seguida, o procedimento Sub verifica cada um dos quatro caixas de entrada na página.  
  
 Como o programa usa a palavra `like` na criação de instruções SQL, as consultas são as pesquisas de subcadeia de caracteres em vez de correspondências exatas.  
  
 Por exemplo, se o **Sobrenome** caixa contida na entrada "Berge" e o **título** contidos de caixa de entrada de "Gerente de programas", a instrução SQL (valor de `myQuery`) lê:  
  
```  
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 Se a consulta for bem-sucedida, todas as pessoas com um sobrenome que contém o texto "Berge" (como Berge e Berger) e com um título que contém as palavras "Gerente de programas" (por exemplo, gerente de programas e tecnologias avançadas) são exibidas na grade de dados HTML.  
  
## <a name="preparing-and-sending-the-query"></a>Preparar e enviando a consulta  
 A última parte do procedimento Sub Find_OnClick consiste em duas instruções. A primeira instrução atribui o [SQL](../../../ado/reference/rds-api/sql-property.md) propriedade o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto igual à consulta do SQL dinamicamente construída. A segunda instrução faz com que o **RDS. DataControl** objeto (`DC1`) para consultar o banco de dados e, em seguida, exibir os novos resultados da consulta na grade.  
  
```  
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>Botão de perfil de atualização  
 Clicando o **atualizar perfil** botão ativa o procedimento de VBScript Update_OnClick Sub, que executa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) e [atualização](../../../ado/reference/rds-api/refresh-method-rds.md) métodos.  
  
```  
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 Quando `DC1.SubmitChanges` é executado, o serviço de dados remoto todas as informações de atualização de pacotes e a envia para o servidor por meio de HTTP. A atualização é tudo ou nada; Se uma parte da atualização for bem-sucedida, nenhuma alteração é feita, e uma mensagem de status é retornada. `DC1.Refresh`não é necessário após **SubmitChanges** com o serviço de dados remoto, mas garante dados atualizados.  
  
## <a name="cancel-changes-button"></a>Botão Cancelar alterações  
 Clicando em **Cancelar alterações** ativa o procedimento de VBScript Cancel_OnClick Sub, que executa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) método.  
  
```  
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 Quando `DC1.CancelUpdate` é executado, ele descarta todas as edições feitas pelo usuário para um registro de funcionário na grade de dados desde a última consulta ou atualização. Restaura os valores originais.  
  
## <a name="see-also"></a>Consulte também  
 [Botões de navegação do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


