# Cardápio Digital

O Cardápio Digital é uma aplicação web moderna que permite aos usuários visualizar itens disponíveis com seus respectivos preços e cadastrar novos produtos de forma fácil e rápida.

## Tecnologias Utilizadas

- Vite
- React
- TypeScript
- @tanstack/react-query

## Instalação

Certifique-se de ter o Node.js e o npm instalados. Clone o repositório e execute o seguinte comando:

```bash
npm install
```

## Como Usar
### Desenvolvimento

Para iniciar o servidor de desenvolvimento:

```bash
npm run dev
```

Isso iniciará o servidor de desenvolvimento do Vite. 

Abra http://localhost:5173 no seu navegador para ver o projeto.

### Produção

Para compilar e construir o projeto para produção:

```bash
npm run build
```

Isso criará uma versão otimizada do seu aplicativo para produção na pasta dist.

## Funcionalidades Principais
- Listar itens do cardápio (GET: utilizando react query - useQuery)
```bash
const fetchData = async (): AxiosPromise<FoodData[]>=> {
    const response = axios.get(API_URL + '/food')
    return response;
}

export function useFoodData() {
    const query = useQuery({
        queryFn: fetchData,
        queryKey: ['food-data'],
        retry: 2
    }) 

    return {
        ...query,
        data: query.data?.data
    }
}
```
- Incluir item no cardápio (POST: Utilizando react query - useMutation)
```bash
const postData = async (data: FoodData): AxiosPromise<unknown>=> {
    const response = axios.post(API_URL + '/food', data)
    return response;
}

export function useFoodDataMutate() {
    const queryClient = useQueryClient();
    const mutate = useMutation({
        mutationFn: postData,
        retry: 2,
        onSuccess: () => {
            queryClient.invalidateQueries({ queryKey: ['food-data']})
        }
    }) 

    return mutate;
}
```
