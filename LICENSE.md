class Solution {
    public int maxTwoEvents(int[][] e) {
        Arrays.sort(e, (a, b) -> Integer.compare(a[1], b[1]));
        int n = e.length;
        int[] dp = new int[n];
        dp[0] = e[0][2];
        for(int i = 1; i < n; i++){
            dp[i] = Math.max(dp[i - 1], e[i][2]);
        }
        int ans = dp[n - 1];
        for (int i = 0; i < n; i++) {
            int l = 0, r = i;
            int maxv = -1;
            while (l <= r) {
                int mid = l + (r - l) / 2;
                if (e[mid][1] < e[i][0]) {
                    maxv = dp[mid];
                    l = mid + 1;
                } else {
                    r = mid - 1;
                }
            }
            if (maxv != -1) {
                ans = Math.max(ans, e[i][2] + maxv);
            }
        }
        return ans;
    }
}
