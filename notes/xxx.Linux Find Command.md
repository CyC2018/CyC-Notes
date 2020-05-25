[Leetcode](https://leetcode.com/discuss/interview-question/369272/Amazon-or-Onsite-or-Linux-Find-Command)

## interface Filter(strategy pattern for SIZE/TYPE filters, decorator pattern for AND/OR/NOT filters) + dfs(if not file) (optimal)
```java
public class Main {
    public class File {
        String name;
        boolean isFile;
        int size;
        String type;
        Map<String, File> files;
        public File(String name, boolean isFile, int size, String type) {
            this.name = name;
            this.isFile = isFile;
            this.size = size;
            this.type = type;
            this.files = new HashMap<>();
        }
    }
    public interface Filter {
        public boolean apply(File file);
    }
    public class MinSizeFilter implements Filter {
        private int minSize;
        public MinSizeFilter(int minSize) {
            this.minSize = minSize;
        }
        @Override
        public boolean apply(File file) {
            return file.size >= minSize;
        }
    }
    public class TypeFilter implements Filter {
        private String type;
        public TypeFilter(String type) {
            this.type = type;
        }
        @Override
        public boolean apply(File file) {
            return this.type.equals(file.type);
        }
    }
    public class NotFilter implements Filter {
        private Filter filter;
        public NotFilter(Filter filter) {
            this.filter = filter;
        }
        @Override
        public boolean apply(File file) {
            return !filter.apply(file);
        }
    }
    public class OrFilter implements Filter {
        private List<Filter> filters;
        public OrFilter(List<Filter> filters) {
            this.filters = filters;
        }
        @Override
        public boolean apply(File file) {
            for (Filter filter : filters) {
                if (filter.apply(file)) return true;
            }
            return false;
        }
    }
    public class AndFilter implements Filter {
        private List<Filter> filters;
        public AndFilter(List<Filter> filters) {
            this.filters = filters;
        }
        @Override
        public boolean apply(File file) {
            for (Filter filter : filters) {
                if (!filter.apply(file)) return false;
            }
            return true;
        }
    }
    public List<File> findWithFilters(File file, List<Filter> filters) {
        List<File> res = new ArrayList<>();
        if (file.isFile) {
            System.out.println("not a directory!");
            return res;
        }
        dfs(file, filters, res);
        return res;
    }
    private void dfs(File file, List<Filter> filters, List<File> res) {
        if (file.files == null) return;
        for (File child : file.files.values()) {
            if (!child.isFile) {
                dfs(child, filters, res);
            } else {
                boolean selectFile = true;
                for (Filter filter : filters) {
                    if (!filter.apply(child)) {
                        selectFile = false;
                    }
                }
                if (selectFile) {
                    res.add(child);
                }
            }
        }
    }
    public void test() {
        File d1 = new File("d1",false,0,"");
        File d1d1 = new File("d1d1",false,0,"");
        d1.files.put(d1d1.name, d1d1);
        File d1f1 = new File("d1f1",true,2,"xml");
        d1.files.put(d1f1.name, d1f1);
        File d1d1f1 = new File("d1d1f1",true,6,"txt");
        d1d1.files.put(d1d1f1.name, d1d1f1);
        File d1d1f2 = new File("d1d1f2",true,3,"txt");
        d1d1.files.put(d1d1f2.name, d1d1f2);
        Filter filter1 = new MinSizeFilter(4);
        Filter filter2 = new TypeFilter("xml");
        Filter filter3 = new OrFilter(Arrays.asList(filter1, filter2));
        List<Filter> filters = Arrays.asList(filter3);
        List<File> res = findWithFilters(d1, filters);
        for (File file : res) {
            System.out.println(file.name);
        }
    }
    public static void main(String[] args) {
        new Main().test();
    }
}
```
