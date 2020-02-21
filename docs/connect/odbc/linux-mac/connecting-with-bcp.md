---
title: Conectar-se com bcp | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1dd80df3a0f7fabec7ae9ddc51b16cb4456c7970
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67996622"
---
# <a name="connecting-with-bcp"></a>Conectando com bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

O utilitário [bcp](https://go.microsoft.com/fwlink/?LinkID=190626) está disponível no [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em Linux e macOS. Esta página documenta as diferenças da versão Windows do `bcp`.
  
- O terminador de campo é um tab (“\t”).  
  
- O terminador de linha é um newline (“\n”).  
  
- O modo de caractere é o formato preferido para arquivos de formato `bcp` e de dados que não contenham caracteres estendidos.  
  
> [!NOTE]  
> Uma barra invertida '\\' em um argumento de linha de comando deve ser colocada entre aspas ou usar caractere de escape. Por exemplo, para especificar uma nova linha como um terminador de linha personalizado, você deve usar um dos seguintes mecanismos:  
>   
> -   -r\\\n  
> -   -r"\n"  
> -   -r'\n'  
  
A seguir está um exemplo de invocação de comando `bcp` para copiar linhas da tabela para um arquivo de texto:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>Opções Disponíveis
Na versão atual, as seguintes sintaxes e opções estão disponíveis:  

[_database_ **.** ]_schema_ **.** _table_ **in** _data\_file_ | **out** _data\_file_

- -a *packet_size*  
Especifica o número de bytes por pacote de rede enviado de e para o servidor.  
  
- -b *batch_size*  
Especifica o número de linhas por lote de dados importados.  
  
- -c  
Usa um tipo de dados de caractere  
  
- -d *database_name*  
Especifica o banco de dados que deve ser conectado.  
  
- -d  
Faz com que o valor passado para a opção -S do `bcp` seja interpretada como um nome da fonte de dados (DSN). Para obter mais informações, consulte "Suporte para SN em sqlcmd e bcp" em [Como conectar-se com sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md).  
  
- -e *error_file* Especifica o caminho completo de um arquivo de erro usado para armazenar as linhas que o utilitário `bcp` não puder transferir do arquivo para o banco de dados.  
  
- -E  
Usa um valor ou valores de identidade no arquivo de dados importados para a coluna de identidade.  
  
- -f *format_file*  
Especifica o caminho completo de um arquivo de formato.  
  
- -f *first_row*  
Especifica o número da primeira linha que deve ser exportada de uma tabela ou importada de um arquivo de dados.  
  
- -k  
Especifica que colunas vazias devem reter um valor nulo durante a operação, em vez de qualquer valor padrão nas colunas inseridas.  
  
- -l  
Especifica um tempo limite de logon. A opção -l especifica o número de segundos antes que um logon em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] expire quando você tentar se conectar a um servidor. O tempo limite de logon padrão é de 15 segundos. O tempo limite do logon deve ser um número entre 0 e 65534. O `bcp` irá gerar uma mensagem de erro se o valor fornecido não for numérico ou não estiver nesse intervalo. Um valor de 0 especifica um tempo limite infinito.
  
- -L *last_row*  
Especifica o número da última linha a ser exportada de uma tabela ou importada de um arquivo de dados.  
  
- -m *max_errors*  
Especifica o número máximo de erros de sintaxe que podem ocorrer antes da operação `bcp` ser cancelada.  
  
- -n  
Usa os tipos de dados nativos (do banco de dados) dos dados para realizar uma operação de cópia em massa.  
  
- -P *password*  
Especifica a senha para a ID de logon.  
  
- -Q  
Executa a instrução SET QUOTED_IDENTIFIERS ON na conexão entre o utilitário `bcp` e uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -r *row_terminator*  
Especifica o terminador de linha.  
  
- -R  
Especifica que dados de moeda, data e horário são copiados em massa no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o formato regional definido para as configurações de localidade do computador cliente.  
  
- -S *server*  
Especifica o nome da instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à qual se conectar ou, se -D é usado, um DSN.  
  
- -t *field_terminator*  
Especifica o terminador de campo.  
  
- -T  
Especifica que o utilitário `bcp` se conecta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com uma conexão confiável (segurança integrada).  
  
- -U *login_id*  
Especifica a ID de logon usada para conectar-se ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -v  
Informa o número de versão e copyright do utilitário `bcp`.  
  
- -w  
Executa a operação de cópia em massa usando caracteres Unicode.  
  
Nesta versão, há suporte para caracteres Latin-1 e UTF-16.  
  
## <a name="unavailable-options"></a>Opções Não Disponíveis
Na versão atual, as seguintes sintaxes e opções não estão disponíveis:  

- -c  
Especifica a página de código dos dados no arquivo de dados.  
  
- -h *hint*  
Especifica as dicas usadas durante uma importação de dados em massa para uma tabela ou exibição.  
  
- -i *input_file*  
Especifica o nome de um arquivo de resposta.  
  
- -n  
Usa os tipos de dados nativos (do banco de dados) dos dados para dados de não caractere e caracteres Unicode para dados de caractere.  
  
- -o *output_file*  
Especifica o nome de um arquivo que recebe a saída redirecionada do prompt de comando.  
  
- -V (80 | 90 | 100)  
Usa tipos de dados de uma versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -X  
Usado com as opções format e -f format_file, gera um arquivo em formato baseado em XML, em vez do arquivo em formato não XML padrão.  
  
## <a name="see-also"></a>Consulte Também

[Conectando com **sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
