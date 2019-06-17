---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 731189838918a04ec211ec0bcac3f66843658177
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699638"
---
# <a name="address-book-command-buttons"></a>Botões de comando do catálogo de endereços
O aplicativo de catálogo de endereços inclui os seguintes botões de comando:  
  
-   Um **localizar** botão para enviar uma consulta ao banco de dados.  
  
-   Um **limpar** botão para limpar as caixas de texto antes de iniciar uma nova pesquisa.  
  
-   Uma **atualizar o perfil** botão para salvar as alterações em um registro de funcionário.  
  
-   Um **Cancelar alterações** botão para descartar as alterações.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="find-button"></a>Botão Localizar  
 Clicar a **localizar** botão ativa o procedimento de VBScript Find_OnClick Sub, que compila e envia a consulta SQL. Clicar nesse botão popula a grade de dados.  
  
## <a name="building-the-sql-query"></a>Criar a consulta SQL  
 A primeira parte do procedimento Sub Find_OnClick compila a consulta SQL, uma só vez, acrescentando cadeias de caracteres de texto para uma instrução de SQL SELECT global. Ele começa definindo a variável `myQuery` para uma instrução SQL SELECT que solicita a todas as linhas de dados da tabela de origem de dados. Em seguida, o procedimento de sub-rotina examina cada uma das quatro caixas de entrada na página.  
  
 Como o programa usa a palavra `like` na criação de instruções SQL, as consultas são as pesquisas de subcadeia de caracteres em vez de correspondências exatas.  
  
 Por exemplo, se o **Sobrenome** caixa contido a entrada "Berge" e o **título** caixa contido a entrada de "Gerente de programas", a instrução SQL (valor de `myQuery`) leria:  
  
```sql
Select FirstName, LastName, Title, Email, Building, Room, Phone from Employee where lastname like 'Berge%' and title like 'Program Manager%'  
```  
  
 Se a consulta foi bem-sucedida, todas as pessoas com um sobrenome que contém o texto "Berge" (como Berge e Berger) e com um título que contêm as palavras "Gerente de programas" (por exemplo, gerente de programa, tecnologias avançadas) são exibidas na grade de dados HTML.  
  
## <a name="preparing-and-sending-the-query"></a>Preparar e enviar a consulta  
 A última parte do procedimento Sub Find_OnClick consiste em duas instruções. A primeira instrução atribui a [SQL](../../../ado/reference/rds-api/sql-property.md) propriedade do [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto igual à consulta SQL criada dinamicamente. A segunda instrução faz com que o **RDS. DataControl** objeto (`DC1`) para consultar o banco de dados e, em seguida, exibir os novos resultados da consulta na grade.  
  
```vb
Sub Find_OnClick  
   '...  
   DC1.SQL = myQuery  
   DC1.Refresh  
End Sub  
```  
  
## <a name="update-profile-button"></a>Botão de perfil de atualização  
 Clicar a **atualizar o perfil** botão ativa o procedimento de VBScript Update_OnClick Sub, que executa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto (`DC1`) [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) e [atualizar](../../../ado/reference/rds-api/refresh-method-rds.md) métodos.  
  
```vb
Sub Update_OnClick  
   DC1.SubmitChanges  
   DC1.Refresh  
End Sub  
```  
  
 Quando `DC1.SubmitChanges` é executado, o serviço de dados remoto todas as informações de atualização de pacotes e o envia para o servidor por meio de HTTP. A atualização é tudo ou nada; Se uma parte da atualização for bem-sucedida, nenhuma alteração é feita, e uma mensagem de status é retornada. `DC1.Refresh` não é necessário após **SubmitChanges** com o serviço de dados remoto, mas garante dados atualizados.  
  
## <a name="cancel-changes-button"></a>Botão Cancelar alterações  
 Clicando em **Cancelar alterações** ativa o procedimento de VBScript Cancel_OnClick Sub, que executa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto (`DC1)` [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) método.  
  
```vb
Sub Cancel_OnClick  
   DC1.CancelUpdate  
End Sub  
```  
  
 Quando `DC1.CancelUpdate` é executado, ele descarta todas as edições que um usuário fez para um registro de funcionário na grade de dados desde a última consulta ou atualização. Ele restaura os valores originais.  
  
## <a name="see-also"></a>Consulte também  
 [Botões de navegação do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)


