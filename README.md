# useDebouncedMemo

> Debounced useMemo().

    yarn add @sevenoutman/use-debounced-memo

## Usage

A common use case is requesting data according to a search input. The controlled `<Input>` updates right as you types, while `searchTodos()` is debounced to 300ms.

```jsx
import useDebouncedMemo from '@sevenoutman/use-debounced-memo';

function App() {
    
    const [todos, setTodos] = useState([]);
    const [search, setSearch] = useState();

    const searchTodos = useCallback(async (searchWord) => {
        const result = await requestTodos(searchWord);
        setTodos(result);
    }, []);

    const debouncedSearch = useDebouncedMemo(() => {
        return search;
    }, [search], 300);

    useEffect(() => {
        searchTodos(debouncedSearch);
    }, [debouncedSearch]);

    return (
        <>
            <Input value={search} onInput={setSearch} />
            <TodoList todos={todos} />
        </>
    );
}
```